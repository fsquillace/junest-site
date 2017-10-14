---
layout: default
---

Usage
=====
There are three different ways you can run JuNest depending on the backend program you decide to use.

PRoot based
-----------
[Proot](https://wiki.archlinux.org/index.php/Proot) represents the default
program used for accessing to the JuNest environments.
The main reason to choose Proot as default backend program is because
it represents a portable solution that works well in most of GNU/Linux distros available.
One of the major drawbacks is the fact that Proot is not officially
supported anymore, therefore, Proot bugs may no longer be fixed.

In order to run JuNest via Proot:

- As normal user - Allow to make basic operations: ```junest```

- As fakeroot - Allow to install/remove packages: ```junest -f```

Linux namespaces based
----------------------
The [Linux namespaces](http://man7.org/linux/man-pages/man7/namespaces.7.html)
represents the next generation backend program for JuNest.
The major drawback about the namespace is portability, as certain requirements
need to be satisfied: 1) Only starting from Linux 3.8, unprivileged processes can
create the required user and mount namespaces.
2) Moreover, the Linux kernel distro must have the user namespace enabled.
Hopefully, in the future the major GNU/Linux distros will start enabling such feature by default.
For instance, Ubuntu (version 12.04+) already has such feature enabled.

In order to run JuNest via Linux namespaces:

- As fakeroot - Allow to install/remove packages: ```junest -u```

Chroot based
------------
This solution suits only for privileged users. JuNest provides the possibility
to run the environment via `chroot` program.
In particular, it uses a special program called `GRoot`, an enhanced `chroot`
wrapper that allows to bind mount directories specified by the user, such as
/proc, /sys, /dev, /tmp and $HOME, before
executing any programs inside the JuNest sandbox. In case the mounting will not
work, JuNest is even providing the possibility to run the environment directly via
the pure `chroot` command.

In order to run JuNest via `chroot` solutions:

- As root via `GRoot` - Allow to have fully root privileges inside JuNest environment (you need to be root for executing this): ```junest -g```

- As root via `chroot` - Allow to have fully root privileges inside JuNest environment (you need to be root for executing this): ```junest -r```

Execution modes comparison table
----------------
The following table shows the capabilities that each backend program is able to perform:

|     | QEMU | Root privileges required | Manage Official Packages | Manage AUR Packages | Portability | Support | User modes |
| --- | ---- | ------------------------ | ------------------------ | ------------------- | ----------- | ------- | ---------- |
| **Proot** | YES | NO | YES | YES | YES | Poor | Normal user and `fakeroot` |
| **Linux Namespaces** | NO | NO | YES | YES | Poor | YES | `fakeroot` only |
| **Chroot** | NO | YES | YES | YES | YES | YES | `root` only |

Advanced usage
==============
## Build image ##
You can build a new JuNest image from scratch by running the following command:

    junest -b [-n]

The script will create a directory containing all the essentials
files in order to make JuNest working properly (such as pacman, yogurt and proot).
The option `-n` will skip the final validation tests if they are not needed.
Remember that the script to build the image must run in an Arch Linux OS with
arch-install-scripts and the base-devel packages installed.
To change the build directory just use the `JUNEST_TEMPDIR` (by default /tmp).

After creating the image junest-x86\_64.tar.gz you can install it by running:

    junest -i junest-x86_64.tar.gz

For more details, you can also take a look at
[junest-builder](https://github.com/fsquillace/junest-builder)
that contains the script and systemd service used for the automatic building
of the JuNest image.

Related wiki page:

- [How to build a JuNest image using QEMU](https://github.com/fsquillace/junest/wiki/How-to-build-a-JuNest-image-using-QEMU)

## Run JuNest using a different architecture via QEMU ##
The following command will download the ARM JuNest image and will run QEMU in
case the host OS runs on either x86\_64 or x86 architectures:

    $> JUNEST_HOME=~/.junest-arm junest -a arm -- uname -m
    armv7l

## Bind directories ##
To bind a host directory to a guest location, you can use proot arguments:

    junest -p "-b /mnt/mydata:/home/user/mydata"

This will works with PRoot, Namespace and GRoot backend programs.
Check out the backend program options by passing `--help` option:

    junest [-u|-g] -p "--help"

## Systemd integration ##
Although JuNest has not been designed to be a complete container, it is even possible to
virtualize the process tree thanks to the [systemd container](https://wiki.archlinux.org/index.php/Systemd-nspawn).
The JuNest containter allows to run services inside the container that can be
visible from the host OS through the network.
The drawbacks of this are that the host OS must use systemd as a service manager,
and the container can only be executed using root privileges.

To boot a JuNest container:

    sudo systemd-nspawn -bD ~/.junest

Related wiki page:

- [How to run junest as a container](https://github.com/fsquillace/junest/wiki/How-to-run-JuNest-as-a-container)
- [How to run services using Systemd](https://github.com/fsquillace/junest/wiki/How-to-run-services-using-Systemd)

Internals
=========

There are two main chroot jail used in JuNest.
The main one is [proot](https://wiki.archlinux.org/index.php/Proot) which
allows unprivileged users to execute programs inside a sandbox and
GRoot, a small and portable version of
[arch-chroot](https://wiki.archlinux.org/index.php/Chroot) which is an
enhanced chroot for privileged users that mounts the primary directories
(i.e. /proc, /sys, /dev and /run) before executing any programs inside
the sandbox.

## Automatic fallback to classic chroot ##
If GRoot fails for some reasons in the host system (i.e. it is not able to
mount one of the directories),
JuNest automatically tries to fallback to the classic chroot.

## Automatic fallback for all the dependent host OS executables ##
JuNest attempt first to run the executables in the host OS located in different
positions (/usr/bin, /bin, /usr/sbin and /sbin).
As a fallback it tries to run the same executable if it is available in the JuNest
image.

## Automatic building of the JuNest images ##
The JuNest images are built every week so that you can always get the most
updated package versions.

## Static QEMU binaries ##
There are static QEMU binaries included in JuNest image that allows to run JuNest
in a different architecture from the host system. They are located in `/opt/qemu`
directory.

Troubleshooting
===============

## Cannot use AUR repository ##

> **Q**: Why do I get the following error when I try to install a package with yogurt?

    Cannot find the gzip binary required for compressing man and info pages.

> **A**: JuNest comes with a very basic number of packages.
> In order to install AUR packages via yogurt you need to install the package group `base-devel` first
> that contains all the essential packages for compiling from source code (such as gcc, make, patch, etc):

    #> pacman -S --ignore sudo base-devel

> Remember to ignore `sudo` as it conflicts with `sudo-fake` package.

## No servers configured for repository ##

> **Q**: Why I cannot install packages?

    #> pacman -S lsof
    Packages (1): lsof-4.88-2

    Total Download Size:    0.09 MiB
    Total Installed Size:   0.21 MiB

    error: no servers configured for repository: core
    error: no servers configured for repository: community
    error: failed to commit transaction (no servers configured for repository)
    Errors occurred, no packages were upgraded.

> **A**: You need simply to update the mirrorlist file according to your location:

    # Uncomment the repository line according to your location
    #> nano /etc/pacman.d/mirrorlist
    #> pacman -Syy

## Locate the package for a given file ##

> **Q**: How do I find which package a certain file belongs to?

> **A**: JuNest is a really small distro, therefore you frequently need to find
> the package name for a certain file. `pkgfile` is an extremely useful package
> that allows you to detect the package of a given file.
> For instance, if you want to find the package name for the command `getopt`:

    #> pacman -S pkgfile
    #> pkgfile --update
    $> pkgfile getop
    core/util-linux

## Kernel too old ##

> **Q**: Why do I get the error: "FATAL: kernel too old"?

> **A**: This is because the binaries from the precompiled package are
> compiled for Linux kernel 2.6.32. When JuNest is started without further
> options, it tries to run a shell from the JuNest chroot. The system sees that
> the host OS kernel is too old and refuses to start the shell.

> The solution is to present a higher "fake" kernel version to the JuNest
> chroot. PRoot offers the *-k* option for this, and JuNest passes this option
> on to PRoot when *-p* is prepended. For example, to fake a kernel version of
> 3.10, issue the following command:

    $> junest -p "-k 3.10"

> As Arch Linux ships binaries for kernel version 2.6.32, the above error is
> not unique to the precompiled package from JuNest. It will also appear when
> trying to run binaries that were later installed in the JuNest chroot with
> the `pacman` command.

> In order to check if an executable inside JuNest chroot is compatible with
> the kernel of the host OS just use the `file` command, for instance:

    $> file ~/.junest/usr/bin/bash
    ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked
    (uses shared libs), for GNU/Linux 2.6.32,
    BuildID[sha1]=ec37e49e7188ff4030052783e61b859113e18ca6, stripped

> The output shows the minimum recommended Linux kernel version.

## Kernel doesn't support private futexes ##

> **Q**: Why do I get the warning: "kompat: this kernel doesn't support private
> futexes and PRoot can't emulate them."?

> **A**: This happens on older host OS kernels when the trick of showing a fake
> kernel version to the JuNest chroot is applied (see above:
> [Kernel too old](#kernel-too-old)).

> The consequence of showing a fake kernel version to the JuNest chroot is that
> in the background, PRoot needs to translate requests from applications in the
> chroot to the old kernel of the host OS. Some of the newer kernel
> functionality can be emulated, but private futexes cannot be translated.

> Private Futexes were introduced in Linux kernel 2.6.22. Therefore, the above
> problem likely appears on old Linux systems, for example RHEL5 systems, which
> are based on Linux kernel 2.6.18. Many of the core tools like `which`, `man`,
> or `vim` run without problems while others, especially XOrg-based programs,
> are more likely to show the warning. These are also more likely to crash
> unexpectedly.

> Currently, there is no (easy) workaround for this. In order to be fully
> compatible with kernels below 2.6.22, both the precompiled package from
> JuNest and all software that is installed later needs to be compiled for this
> kernel. Most likely this can only be achieved by building the needed software
> packages from source, which kind of contradicts JuNest's distro-in-a-distro
> philosophy.

## SUID permissions ##
> **Q**: Why I do not have permissions for ping?

    $> ping www.google.com
    ping: icmp open socket: Operation not permitted

> **A**: The ping command uses *suid* permissions that allow to execute the command using
> root privileges. The fakeroot mode is not able to execute a command set with suid,
> and you may need to use root privileges. There are other few commands that
> have *suid* permission, you can list the commands from your JuNest environment
> with the following command:

    $> find /usr/bin -perm +4000

## No characters are visible on a graphic application ##

> **Q**: Why I do not see any characters in the application I have installed?

> **A**: This is probably because there are no
> [fonts](https://wiki.archlinux.org/index.php/Font_Configuration) installed in
> the system.

> To quick fix this, you can just install a fonts package:

    #> pacman -S gnu-free-fonts

## Differences between filesystem and package ownership ##

> **Q**: Why do I get warning when I install a package using root privileges?

    #> pacman -S systat
    ...
    warning: directory ownership differs on /usr/
    filesystem: 1000:100  package: 0:0
    ...

> **A**: In these cases the package installation went smoothly anyway.
> This should happen every time you install package with root privileges
> since JuNest will try to preserve the JuNest environment by assigning ownership
> of the files to the real user.

## Not enabled User namespace or kernel too old ##

> **Q**: Why do I get warning when I run JuNest via Linux namespaces?

    $> junest -u
    User namespace is not enabled or Kernel too old (<3.8). Proceeding anyway...

> **A**: This means that JuNest detected that the host OS either
> does not have a newer Linux version or the user namespace is not enabled.
> JuNest does not stop the execution of the program but it attempts to run it
> anyway. Try to use Proot as backend program in case is not possible to invoke namespaces.

More documentation
==================
There are additional tutorials in the
[JuNest wiki page](https://github.com/fsquillace/junest/wiki).
