---
title: JuNest on different architectures
layout: default
---

JuNest can now emulates any images for x86, x86\_64 and arm architectures!
The neat syntax is the following:

    junest -a arm

For instance, on a x86\_64 machine the previous command will download
the ARM JuNest image and will run QEMU to emulate it!
<!--more-->

There are plenty of reasons this might be useful. For instance, this feature
will give great benefits for developers/people without privileged
permissions on the machine that need to test/use applications on
different architectures. Another advantage is that, there might be packages
available only on some specific architectures that the users can still use
even though the native architecture is different.

{% include comments.html%}
