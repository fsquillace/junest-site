---
layout: default
---

Quickstart
==========
There are three different ways you can run JuNest:

- As normal user - Allow to make basic operations: ```junest```

- As fakeroot - Allow to install/remove packages: ```junest -f```

- As root - Allow to have fully root privileges inside JuNest environment (you need to be root for executing this): ```junest -r```

If the JuNest image has not been downloaded yet, the script will download
the image and will place it to the default directory ~/.junest.
You can change the default directory by changing the environment variable *JUNEST\_HOME*.

If you are new on Archlinux and you are not familiar with *pacman* package manager
visit the [pacman rosetta page](https://wiki.archlinux.org/index.php/Pacman_Rosetta).

Installation
============

## Dependencies ##
JuNest comes with a very short list of dependencies in order to be installed in most
of GNU/Linux distributions.
Before installing JuNest be sure that all dependencies are properly installed in your system:

- [bash (>=4.0)](https://www.gnu.org/software/bash/)
- [GNU coreutils](https://www.gnu.org/software/coreutils/)

The minimum recommended Linux kernel is 2.6.0+ on x86 32 and 64 bit and ARM architectures.

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
    curl https://dl.dropboxusercontent.com/u/42449030/junest/junest-${ARCH}.tar.gz | tar -xz -C ~/.junest
    export PATH=~/.junest/opt/junest/bin:$PATH

### Direct downloads ###
{% include download-links.html %}

   JuNest images for each architecture.
