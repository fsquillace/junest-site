---
title: JuNest and Systemd
layout: default
---

{{page.title}}
==============

Starting from systemd version 226 is now easy to create
[user-specific unit services](https://www.archlinux.org/news/d-bus-now-launches-user-buses/).
<!--more-->

This means that a normal user can now manage his own systemd unit services
without the need to be root. For more information on how to create
user-specific unit services take a look at
[here](https://wiki.archlinux.org/index.php/Systemd/User).

There are several nice advantages for creating a unit service with systemd:

- There is no need to keep a JuNest session opened in order to have a service running. The JuNest session will be handled by systemd service itself;
- The service can be started as soon as the user will log in;
- The [systemd/Timers](https://wiki.archlinux.org/index.php/Systemd/Timers) can be used

With JuNest you can create a systemd unit service based on a service installed
in your JuNest environment. For instance, the following link shows how
to create the dropbox service installed in JuNest and to get it started
every time the user log in to the system:

- [How to run services using Systemd](https://github.com/fsquillace/junest/wiki/How-to-run-services-using-Systemd)

{% include comments.html%}
