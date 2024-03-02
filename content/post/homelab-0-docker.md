+++
title = "Homelab Part 0: Docker on Raspberry Pi"
date = "2024-02-25T22:11:46+02:00"
type = "post"
+++

This weekend I set up a new homelab. Basically a way for me to [self-host](https://github.com/awesome-selfhosted/awesome-selfhosted) some services that I use while running my own personal tech playground.

I already have this setup with a Raspberry Pi 3 where I have a few things set up in an old school fashion of running services like daemons and running everything behind an Apache2 server. There are some benefits to this in that the setup is pretty straightforward and simple to understand without layers and abstractions but the downside is the maintenance. Upgrading services is a chore and a very manual process.

So, with the new Raspberry Pi 5 I wanted to do something different. With a containerized setup upgrades can be done by simply replacing image tags. If I want to try something up it is incredibly easy to set up and tear down. It is also not much more work to set up than what the more barebones approach requires.

These are some notes from my adventure below. I intend to write follow up posts of additional things I get set up and the steps to get there.

## Preparing the Raspberry Pi

What was really nice here since the last time I installed a Raspberry Pi is that the tooling is a lot stronger. Now there is an [imager tool](https://www.raspberrypi.com/software/) that does a lot of the heavy lifting for us. Yet another app to install though but in my opinion a lot clearer than the old ways of `dd if=raspbian.img of=/dev/sdx`.

A pretty big gotcha here though is that not only is the SSH server no longer enabled by default. The default `pi` user has been removed also. This requires some configuration to be done in advance for a headless setup. Luckily the imager has [settings for enabling all of this](https://www.raspberrypi.com/documentation/computers/getting-started.html#install-using-imager).

## Setting up Docker

Getting Docker set up is super easy. All it boils down to is basically the following.

```bash
$ curl -sSL https://get.docker.com | sh
$ sudo usermod -aG docker $USER
```

This can then be tested by running a tiny container to see that everything works.

```bash
docker run hello-world
```

## Managing stuff with Portainer

Running the server through SSH and CLI commands works. But it is nice to have a decent interface to get a better overview of things. Portainer plugs in nicely with Docker and allows setting up stacks through docker-compose files and managing individual containers.

The tricky part that I found here is that there is a business edition and a community edition. The instructions are also different based on your setup so it is important to find the right page. For me this was [Install Portainer CE with Docker on Linux](https://docs.portainer.io/start/install-ce/server/docker/linux).

The setup itself is as easy as installing Docker.

```bash
docker volume create portainer_data
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

## Next steps

Next I want to add some centralized authentication so that I do not need to set up user and password for every single service. That means single-sign on (SSO) with OAuth but it also means that I will need a database to store the users and a database means PostgreSQL.
