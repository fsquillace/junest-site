---
layout: default
---

Quickstart
==========
The basic way to run JuNest is via the [Proot](https://wiki.archlinux.org/index.php/Proot) as the backend program:

- As normal user - Allow to make basic operations: ```junest```

- As fakeroot - Allow to install/remove packages: ```junest -f```

To know more about the JuNest execution modes depending on the backend program
used, see the [Usage](#usage) section below.

After running JuNest
--------------------
If the JuNest image has not been downloaded yet, the script will download
the image from the repository and will place it to the default directory `~/.junest`.
You can change the default directory by changing the environment variable `JUNEST_HOME`.

If you are new on Arch Linux and you are not familiar with `pacman` package manager
visit the [pacman rosetta page](https://wiki.archlinux.org/index.php/Pacman_Rosetta).

Installation
============

## Dependencies ##
JuNest comes with a very short list of dependencies in order to be installed in most
of GNU/Linux distributions.
Before installing JuNest be sure that all dependencies are properly installed in your system:

- [bash (>=4.0)](https://www.gnu.org/software/bash/)
- [GNU coreutils](https://www.gnu.org/software/coreutils/)

The minimum recommended Linux kernel of the host OS is 2.6.32 on x86 (32-bit
and 64 bit) and ARM architectures. It is still possible to run JuNest on lower
2.6.x host OS kernels but errors may appear, and some applications may
crash. For further information, read the [Troubleshooting](#troubleshooting)
section below.


## Method one (Recommended) ##
Just clone the JuNest repo somewhere (for example in ~/.local/share/junest):

    git clone git://github.com/fsquillace/junest ~/.local/share/junest
    export PATH=~/.local/share/junest/bin:$PATH

### Installation using AUR (Arch Linux only) ###
If you are using an Arch Linux system you can, alternatively, install JuNest from the [AUR repository](https://aur.archlinux.org/):

    yaourt -S junest-git
    export PATH=/opt/junest/bin:$PATH

## Method two ##
Alternatively, another installation method would be to directly download the JuNest image and place it to the default directory ~/.junest:

    ARCH=<one of "x86_64", "x86", "arm">
    mkdir ~/.junest
    curl https://s3-eu-west-1.amazonaws.com/junest-repo/junest/junest-${ARCH}.tar.gz | tar -xz -C ~/.junest
    export PATH=~/.junest/opt/junest/bin:$PATH

### Direct downloads ###
{% include download-links.html %}

   JuNest images for each architecture.
