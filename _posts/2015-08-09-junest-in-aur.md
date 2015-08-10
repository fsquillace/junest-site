---
title: JuNest is now in AUR!
layout: default
---

JuNest is now available in
[AUR](https://wiki.archlinux.org/index.php/Arch_User_Repository) repository.
This means that you can easily install JuNest inside an Arch Linux based
system with the following command:

    yaourt -S junest-git
<!--more-->

An additional benefit is that
[_junest-git_](https://aur.archlinux.org/packages/junest-git/) package is also used to build
the JuNest image. Previously, the JuNest script were copied in the directory
`/opt/junest/` using git command. The problem was that the JuNest script could
not be easily updated. Now, inside a JuNest environment, it is possible
to update JuNest with the most recent changes by just upgrading the
[_junest-git_](https://aur.archlinux.org/packages/junest-git/) package.

{% include comments.html%}
