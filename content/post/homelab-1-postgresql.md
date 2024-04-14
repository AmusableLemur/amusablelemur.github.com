+++
title = "Homelab Part 1: Database Backend"
date = "2024-03-03T10:00:00+02:00"
type = "post"
+++

Before I can set up any services I will need to have some method of authentication and for that I need somewhere to store user information. This could technically be a simple SQLite database but since PostgreSQL is useful for other things I might as well start here.

## Preparing PostgreSQL

What is really nice about adding a stack in Portainer is how it is just a docker-compose file that can be copy-pasted directly into the interface. This also makes it easy to keep related services up to date in the same file.

PostgreSQL uses semantic versioning so setting the image to `postgres:16` will make sure I still get new features e.g. upgrade from 16.2 to 16.3 when that becomes available. I could also use `postgres:latest` or simply `postgres` to have the same effect but that will also replace my stack with 17.0 at some point and I do not trust that an automatic upgrade will be seamless.

Instead of exposing the port on the host I will use a bridge network to limit who has access to PostgreSQL. This reduces the attack vector a bit with the downside that the databases will only be available to containers running on this machine.

## Administrating PostgreSQL with PGAdmin4

Initially I did not want a tool for Postgres but it turned out to be so incredibly cumbersome to create tables and users by connecting to the container and running the CLI so I caved and added PGadmin to the stack.

This uses a similar setup to PostgreSQL and is added to the same docker-compose file. It connects to the database through the bridge network but here I also expose the containers port 80 on the hosts port 5050.

```yaml
ports:
  - "5050:80"
networks:
  - postgres
```

This way I can connect directly to PGAdmin4 without a proxy. While this is not exactly great for security it is constrained to the internal network behind a NAT and firewall and it also uses a strong username and password similar to Portainer.
