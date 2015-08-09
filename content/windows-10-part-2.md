+++
title = "Windows 10 part 2"
date = "2015-08-06T22:44:03+02:00"
type = "post"
+++

Another problem with Windows 10. It turns out that there's a race condition in
VirtualBox where host-only adapters cannot be created and just fails with a
(very) generic error message.

It's all documented in [#14040](https://www.virtualbox.org/ticket/14040) on
their issue tracker. Where, luckily, Yirkha has provided a temporary fix until
the bug can be patched upstream. Downloading and running it in the background
as per his instructions should solve the issue.

In the odd case that your virtual networks still aren't working you've probably
ended up with two or more identical adapters like I did. Just go to the
VirtualBox interface, find the global settings in the menu and delete any
network adapter not in use.
