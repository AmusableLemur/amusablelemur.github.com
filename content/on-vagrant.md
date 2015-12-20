---
date: "2014-01-31"
title: On Vagrant
type: post
---

Vagrant enables a developer to isolate their project to a dedicated virtual machine while still coding in the same environment they use for other projects. You can essentially edit your project files in Windows and access the result through Windows while everything is running on Linux without having to do any of the tedious work of setting up and installing a virtual machine.

The cool thing about Vagrant is how the configuration file for the project can be redistributed with the rest of the code base to give other developers access to an exact replica of the original development environment.

The really cool thing about Vagrant is how ridiculously easy it is, they have a [guide][1] for setting up a first project which takes about 30 minutes to complete and goes over all the aspects of setting everything up.

The major thing that bothers me is that it's somewhat slow, a virtual machine has a huge overhead compared to running directly on the host machine. It also takes about fifteen minutes to set up a Vagrant box the first time, which is actually negligent compared to the many hours it would take to do it manually but still feels like a long time.

Provisioning could also have been made simpler, but there are a lot of alternatives and even more examples for setting up any imaginable environment so it isn't really a problem per se.

 [1]: http://docs.vagrantup.com/v2/getting-started/index.html
