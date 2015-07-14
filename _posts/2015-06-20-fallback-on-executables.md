---
title: JuNest runs on exotic environments
layout: default
excerpt_separator: <!--more-->
---

JuNest can even run in the most exotic environments!
==============

One of the most important aspects of JuNest is that it must run even
on exotic host systems. This JuNest principle implies that many failure cases
need to be taken into account. For instance, JuNest must use a limited number of
unix commands in order to have more chances of portability
on heterogeneous systems.

In the last release, the JuNest portability has been drastically
increased thanks to a reliable fallback mechanism.
Each executables used inside the JuNest scripts is wrapped
by bash functions that first check if the executables is available
in any of the host system paths (i.e. /bin, /usr/bin, /usr/sbin and /sbin).
In case the executable returns a bad exit code, JuNest will try to run
the same executable available inside the JuNest image as last hope.

This approach has brought to a big improvements, for instance it is now possible
to have JuNest running even on really small OS such as
[Tiny Core Linux](http://distro.ibiblio.org/tinycorelinux/).

There are only eight needed executables for JuNest: `bash`,
`chown` (for root access only), `ln`, `mkdir`, `rm`, `tar`, `uname` and
either `wget` or `curl`.
