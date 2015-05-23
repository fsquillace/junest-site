---
layout: default
---

Advanced usage
============

## Build image ##
You can build a new JuJube image from scratch by running the following command:

    jujube -b [-n]

The script will create a directory containing all the essentials
files in order to make JuJube working properly (such as pacman, yaourt, arch-chroot and proot).
The option **-n** will skip the final validation tests if they are not needed.
Remember that the script to build the image must run in an Arch Linux OS with
arch-install-scripts, package-query, git and the base-devel packages installed.
To change the build directory just use the *JUJUBE_TEMPDIR* (by default /tmp).

After creating the image jujube-x86\_64.tar.gz you can install it by running:

    jujube -i jujube-x86_64.tar.gz

Related wiki page:

- [How to build a JuJube image using QEMU](https://github.com/fsquillace/jujube/wiki/How-to-build-a-JuJube-image-using-QEMU)

## Bind directories ##
To bind a host directory to a guest location, you can use proot arguments:

    jujube -p "-b /mnt/mydata:/home/user/mydata"

Check out the proot options with:

    jujube -p "--help"

##Automatic fallback to classic chroot##
Since the [arch-chroot](https://wiki.archlinux.org/index.php/Chroot) may not work
on some distros, JuJube automatically tries to fallback to the classic chroot.

## JuJube as a container ##
Although JuJube has not been designed to be a complete container, it is even possible to
virtualize the process tree thanks to the [systemd container](https://wiki.archlinux.org/index.php/Systemd-nspawn).
The JuJube containter allows to run services inside the container that can be
visible from the host OS through the network.
The drawbacks of this are that the host OS must use systemd as a service manager,
and the container can only be executed using root privileges.

To boot a JuJube container:

    sudo systemd-nspawn -bD ~/.jujube

Related wiki page:

- [How to run jujube as a container](https://github.com/fsquillace/jujube/wiki/How-to-run-JuJube-as-a-container)

Troubleshooting
===============

##Cannot use AUR repository##

> **Q**: Why do I get the following error when I try to install a package with yaourt?

    Cannot find the gzip binary required for compressing man and info pages.

> **A**: JuJube comes with a very basic number of packages.
In order to install packages using yaourt you may need to install the package group **base-devel**
that contains all the essential packages for compiling source code (such as gcc, make, patch, etc):

    pacman -S base-devel

##Kernel too old##

> **Q**: Why do I get the error: "FATAL: kernel too old"?

> **A**: This is because the executable from the precompiled package cannot
properly run if the kernel is old.
JuJube contains two different PRoot binaries, and one of them is highly compatible
with old linux kernel versions. JuJube will detect which PRoot binary need to be
executed but you may need to specify the PRoot *-k* option if the guest rootfs
requires a newer kernel version:

    jujube -p "-k 3.10"

In order to check if an executable inside JuJube environment can be compatible
with the kernel of the host OS just use the *file* command, for instance:

    file ~/.jujube/usr/bin/bash
    ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked
    (uses shared libs), for GNU/Linux 2.6.32,
    BuildID[sha1]=ec37e49e7188ff4030052783e61b859113e18ca6, stripped

From the output you can see what is the minimum recommended Linux kernel version.

##SUID permissions##
> **Q**: Why I do not have permissions for ping?

    ping www.google.com
    ping: icmp open socket: Operation not permitted

> **A**: The ping command uses *suid* permissions that allow to execute the command using
root privileges. The fakeroot mode is not able to execute a command set with suid,
and you may need to use root privileges. There are other few commands that
have *suid* permission, you can list the commands from your JuJube environment
with the following command:

    find /usr/bin -perm +4000

##No characters are visible on a graphic application##

> **Q**: Why I do not see any characters in the application I have installed?

> **A**: This is probably because there are no
[fonts](https://wiki.archlinux.org/index.php/Font_Configuration) installed in
the system.

To quick fix this, you can just install a fonts package:

    pacman -S gnu-free-fonts

##Differences between filesystem and package ownership##

> **Q**: Why do I get warning when I install a package using root privileges?

    pacman -S systat
    ...
    warning: directory ownership differs on /usr/
    filesystem: 1000:100  package: 0:0
    ...

> **A**: In these cases the package installation went smoothly anyway.
This should happen every time you install package with root privileges
since JuJube will try to preserve the JuJube environment by assigning ownership
of the files to the real user.

##No servers configured for repository##

> **Q**: Why I cannot install packages?

    pacman -S lsof
    Packages (1): lsof-4.88-2

    Total Download Size:    0.09 MiB
    Total Installed Size:   0.21 MiB

    error: no servers configured for repository: core
    error: no servers configured for repository: community
    error: failed to commit transaction (no servers configured for repository)
    Errors occurred, no packages were upgraded.

> **A**: You need simply to update the mirrorlist file according to your location:

    # Uncomment the repository line according to your location
    nano /etc/pacman.d/mirrorlist
    pacman -Syy

More documentation
==================
There are additional tutorials in the
[JuJube wiki page](https://github.com/fsquillace/jujube/wiki).

