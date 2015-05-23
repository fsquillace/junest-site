---
layout: default
---

Quickstart
==========
There are three different ways you can run JuJube:

- As normal user - Allow to make basic operations using [proot](https://wiki.archlinux.org/index.php/Proot): ```jujube```

- As fakeroot - Allow to install/remove packages using [proot](https://wiki.archlinux.org/index.php/Proot): ```jujube -f```

- As root - Allow to have fully root privileges inside JuJube environment using [arch-chroot](https://wiki.archlinux.org/index.php/Chroot) (you need to be root for executing this): ```jujube -r```

If the JuJube image has not been downloaded yet, the script will download
the JuJube image and will place it to the default directory ~/.jujube.
You can change the default directory by changing the environment variable *JUJUBE\_HOME*.

If you are new on Archlinux and you are not familiar with *pacman* package manager
visit the [pacman rosetta page](https://wiki.archlinux.org/index.php/Pacman_Rosetta).

Installation
============
JuJube can works on GNU/Linux OS with kernel version greater or equal
2.6.0 (JuJube was not tested on kernel versions older than this) on 64 bit, 32 bit and ARM architectures.

## Method one (Recommended) ##
Just clone the JuJube repo somewhere (for example in ~/jujube):

    git clone git://github.com/fsquillace/jujube ~/jujube
    export PATH=~/jujube/bin:$PATH

## Method two ##
Alternatively, another installation method would be to directly download the JuJube image and place it to the default directory ~/.jujube:

    ARCH=<one of "x86_64", "x86", "arm">
    mkdir ~/.jujube
    curl https://dl.dropboxusercontent.com/u/42449030/jujube/jujube-${ARCH}.tar.gz | tar -xz -C ~/.jujube
    export PATH=~/.jujube/opt/jujube/bin:$PATH

###Direct downloads###
{% include download-links.html %}

   JuJube images for each architecture.

Dependencies
============
JuJube comes with a very short list of dependencies in order to be installed in most
of GNU/Linux distributions. The needed executables in the host OS are:

- bash
- wget or curl
- tar
- mkdir
- ln
- chown (for root access only)

The minimum recommended linux kernel is 2.6.0+
