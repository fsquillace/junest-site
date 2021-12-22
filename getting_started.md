---
layout: default
---

Quickstart
==========

Setup environment
-----------------

The first operation required is to install the JuNest environment in the
location of your choice (by default `~/.junest`, configurable via the environment variable `JUNEST_HOME`):

```sh
junest setup
```

The script will download the image from the repository and will place it to the default directory `~/.junest`.

Access to environment
---------------------

JuNest uses the Linux namespaces (aka `ns`) as the default backend program. To access via `ns` just type:

```sh
junest
```

You can use the command `sudo` to acquire fakeroot privileges and
install/remove packages.

Alternatively, you can access fakeroot privileges without using `sudo` all the
time with the `-f` (or `--fakeroot`) option:

```sh
junest -f
```

Another execution mode is via [Proot](https://wiki.archlinux.org/index.php/Proot):

```sh
junest proot [-f]
```

There are multiple backend programs, each with its own pros/cons.
To know more about the JuNest execution modes depending on the backend program
used, see the [Usage](#usage) section below.

Run JuNest installed programs directly from host OS
---------------------------------------

Installed programs can be accessible directly from host without
calling `junest` command.
For instance, supposing the host OS is an Ubuntu distro you can directly
run `pacman` by simply updating the `PATH` variable:

```sh
export PATH="$PATH:~/.junest/usr/bin_wrappers"
pacman -S htop
htop
```

By default the wrappers use `"ns --fakeroot"` but you can change it via `JUNEST_ARGS` environment variable.
For instance, if you want to run `iftop` with real root privileges:

```
pacman -S iftop
sudo JUNEST_ARGS="groot" iftop
```

Install packages from AUR
-------------------------

In `ns` mode, you can easily install package from [AUR](https://aur.archlinux.org/) repository
using the already available [`yay`](https://aur.archlinux.org/packages/yay/)
command. In `proot` mode, JuNest does no longer support the building of AUR packages.

**Remember** that in order to build packages from AUR, `base-devel` package group is required
first:

```sh
pacman -Syu --ignore sudo base-devel
:: sudo is in IgnorePkg/IgnoreGroup. Install anyway? [Y/n] n
...
...
```

JuNest uses a modified version of `sudo`. That's why the original `sudo`
package **must be ignored** in the previous command.

Have fun!
---------

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

## Installation from git repository ##
Just clone the JuNest repo somewhere (for example in ~/.local/share/junest):

```sh
git clone https://github.com/fsquillace/junest.git ~/.local/share/junest
export PATH=~/.local/share/junest/bin:$PATH
```

Optionally you want to use the wrappers to run commands
installed in JuNest directly from host:

```sh
export PATH="$PATH:~/.junest/usr/bin_wrappers"
```
Update your `~/.bashrc` or `~/.zshrc` to get always the wrappers available.

### Installation using AUR (Arch Linux only) ###
If you are using an Arch Linux system you can, alternatively, install JuNest from the [AUR repository](https://aur.archlinux.org/packages/junest-git/).
JuNest will be located in `/opt/junest/`

