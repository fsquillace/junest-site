---
title: Everything starts from zero! (MUST READ)
layout: default
---

This is the first (and hopefully not last) blog post for
JuNest. Generally, I will use the blog posts to provide news, anecdote
and stories informally about this project. For this particular blog post
I will explain the reasons that brought me to build JuNest, how it was born
and why I decided to give that name. Despite of my bad English
I hope you will enjoy this article anyway.
<!--more-->

The reasons
-----------

This project was born when I tried to answer to these questions:

>Why is it needed to be root inside a GNU/Linux environment for installing packages?  
>Can I have a sandbox for doing whatever I want without messing up the rest of the system?

In this section I want to provide some example which
will help me to convince you how useful JuNest could be for plenty of purposes.

The first example I want to mention is probably the most important one.
Let's suppose you have unprivileged access to a system of your
University/Company that you use for your project. This is a fairly common
scenario for people that work on research activities to have access on a very
powerful system/cluster. Eventually, you will end up with one need: install all the packages
your program depends on.
In these cases you have two choices: 1) Ask to the administrator if the needed
packages can be installed, 2) compile and install the needed software in your home directory.
None of those choices are a pleasure to deal with. Trust me. If the software
you need to install is quite common the option 1) might the easiest solution,
but sometimes it is hard to predict the packages that will be needed and, at the end,
you might end up to require several times package approvals to the administrator.
Nevertheless, it is needed a bit of time (even days or week) in order
to get the packages approved which can be quite annoying if you have to
deliver your software soon!
The option (2 can be a good choice in case the program you need does not have
many dependencies. Now, let's try to be honest, how many people had always
succeeded to install a fairly complex source code with at least one dependency
on another source code. You can succeed once but not all the times
and there could be plenty of reasons why.
For example, if the gcc compiler is old (likely to happen since
CentOS servers usually have a really old repository)
the compilation might not work; the Makefile requires few changes to make
the dependency visible during the compilation process; there might be a chain
of dependencies that would require to spend all the day to get things working;
you might need to compile the code using a different architecture from the
native one and so on.
This is probably the major reason you really want to know about JuNest but
there are also other interesting reasons which you would love to know.

Let's suppose you have a system in production with a web server on it that is
currently taking traffic. Depending on the availability of your service, it
might be scaring to even ssh to the host and change some config files.
Sometimes it is also useful to use some monitoring system
commands to check the status of the machine and, for getting them you would
end up to install some packages too. The idea of installing packages might looks
harmless but actually you could break a lot of stuff. For instance, after a package
is installed one of the configuration files in /etc might be altered so that
your web server will not start at boot, or the hosts file will be changed so
that the service cannot reach one of the external service which it depends on.
The thing might get even worse if the package you are installing contains a
security vulnerability that would allow unprivileged remote access to your machine
giving visibility of data stored in the filesystem!

Another reason you might end up choosing JuNest is when you want to have
a portable GNU/Linux environment to bring always with you so that you can run
your program on any machine.

Most of the use case scenarios I mentioned previously can be easily solved thanks
to JuNest. You can get your own sandbox inside your home directory, install all
the packages you need and run them!

The origins
-----------

The initial idea behind this was to have a sort of mini
[pacman](https://wiki.archlinux.org/index.php/Pacman) developed in bash
used to install package inside a specific directory in home.
This script (available [here](https://github.com/fsquillace/juju-old)) was
capable of both downloading the PKGBUILD file of the package and
of installing the package plus all the related dependencies. It was even able
to work with the AUR packages.
In order to create a sandbox, I used fakechroot in combination with
fakeroot to provide an environment for faking the root privileges.

This approach was pretty interesting and exciting to me since I was able to
have a portable pacman to use everywhere I needed. The drawback of this project
was that sometimes the script could not work for package groups and the PKGBUILD
specification changed along the time, so that the script was able to work only
for some packages. At the end, I had to give up with this approach and so
I failed miserably...

After this failed experience, things got pretty interesting.
In fact, I realized that the approach can be simpler. Instead of writing a pacman
from scratch I could just use and jail the existing pacman inside a sandbox
within a bunch of scripts that do all the magic on it. I started building an
extremely minimal version of Arch Linux using the pacstrap script with just
few essential packages to make the rootfs usable. After that, instead of having
the sandbox based on fakechroot I used the great [proot](http://proot.me/) which
solved both the need of faking the environment and the mounting of
the main directories.
Later on, I combined everything with additional scripts that made easier for
the final user to download the image and, in particular, to ensure
the portability of the environment even in stunted host systems.

The result of this is now called JuNest and, at the time of writing, I have
just realizing that coincidentally the JuNest's
[first commit date](https://github.com/fsquillace/junest/commit/397d941141d4b5be96a1f0a93cf44fd78528a3a6) correspond to the
[Github birthday](http://tom.preston-werner.com/2008/10/18/how-i-turned-down-300k.html).
Sometimes, fate make easily fun of us.

What's your name?
-----------

As a last topic of this first blog post about JuNest I would like to talk about
its name. Originally, I did not have any doubt about the name of this project.
"It clearly must be called JuJu!" Yes, that is what I said the first day this
project came into my mind. It was almost like the idea and the name were bind
conceptually together for me, for some reason.

The JuJu name is not just a casual name that came in my mind but it actually
has a meaning for me. Few years ago I usually met my nerd friends in a bar
called "JuJu" exchanging thoughts, opinions and ideas with them mostly
about the IT world and that was the reason why I tightly wanted to use that
name for this project.

As you probably already understood, suddenly a terrible news arrived.
JuJu already exists in another project, and this project is not something
small. It is the name used to identify the Canonical product Juju (note that
there is only one letter "J" uppercase). Afterward, I was not so upset because I
knew this project could not be compared to a Canonical product in
terms of popularity by any means. So, nobody could ever complain
about name clashes from an unknown project like mine. Indeed, the estimation
about the popularity of this project that I gave was a bit wrong. People
started watching the project, giving me useful suggestions and make interesting
contributions. Magically, the machine started to work, it just needed
to be well-oiled.

Later on, another terrible news arrived that I did not realized at the beginning.
Canonical has a registered trademark on JUJU.
At this point since the project grew up pretty quickly I decided, after a big
effort made, to change the name to JuJube, to avoid any kind of troubles
with the trademarks. The relevant advantages that brought me to choose
the word JuJube were:

- The original meaning is preserved (The JuJu pub)
- By searching in [trademark site](https://www.ipo.gov.uk/tmtext.htm) there are no similar trademarks with JuJube
- Jujube is a fruit that will be used to identify the distro so this also reduce by far any confusion with the Canonical product

It turned out that neither this was enough to fix the troubles. I got an email
from Canonical stating that the JuJube name might be confusing and they
suggested me to change the name to something else.

At the end I gave up the battle and I decided to choose another name. After
almost two weeks of effort for finding a name, I finally decided to name the
project JuNest. The word "nest" reflects the fact that the distro is a small
size sandbox, and the "Ju" stands for "Jailed user", which is the condition
that an unprivileged user is inside a given GNU/Linux system.

Even tough the new name does not preserve completely the original meaning
I am still happy that, at least, it does contain a meaning about what the
distro actually does.

Starting to realize that this blog is too long so, I conclude by saying thanks to
everybody that does and will do contributions to this project. Hope you will
like the name and the distro!

{% include comments.html%}
