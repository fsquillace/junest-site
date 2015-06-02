---
layout: default
---

Quickstart
==========
There are three different ways you can run JuNest:

- As normal user - Allow to make basic operations using [proot](https://wiki.archlinux.org/index.php/Proot): ```junest```

- As fakeroot - Allow to install/remove packages using [proot](https://wiki.archlinux.org/index.php/Proot): ```junest -f```

- As root - Allow to have fully root privileges inside JuNest environment using [arch-chroot](https://wiki.archlinux.org/index.php/Chroot) (you need to be root for executing this): ```junest -r```

If the JuNest image has not been downloaded yet, the script will download
the JuNest image and will place it to the default directory ~/.junest.
You can change the default directory by changing the environment variable *JUNEST\_HOME*.

If you are new on Archlinux and you are not familiar with *pacman* package manager
visit the [pacman rosetta page](https://wiki.archlinux.org/index.php/Pacman_Rosetta).

Installation
============
JuNest can works on GNU/Linux OS with kernel version greater or equal
2.6.0 (JuNest was not tested on kernel versions older than this) on 64 bit, 32 bit and ARM architectures.

## Method one (Recommended) ##
Just clone the JuNest repo somewhere (for example in ~/junest):

    git clone git://github.com/fsquillace/junest ~/junest
    export PATH=~/junest/bin:$PATH

## Method two ##
Alternatively, another installation method would be to directly download the JuNest image and place it to the default directory ~/.junest:

    ARCH=<one of "x86_64", "x86", "arm">
    mkdir ~/.junest
    curl https://dl.dropboxusercontent.com/u/42449030/junest/junest-${ARCH}.tar.gz | tar -xz -C ~/.junest
    export PATH=~/.junest/opt/junest/bin:$PATH

###Direct downloads###
{% include download-links.html %}

   JuNest images for each architecture.

Dependencies
============
JuNest comes with a very short list of dependencies in order to be installed in most
of GNU/Linux distributions. The needed executables in the host OS are:

- bash
- wget or curl
- tar
- mkdir
- ln
- chown (for root access only)

The minimum recommended linux kernel is 2.6.0+