---
title: JuNest Linux
layout: default
---

JuNest
======
The lightweight Arch Linux based distro that runs, without root privileges, upon any Linux distro.

{% include star-me.html %}

|Project Status|Donation|Communication|
|:------------:|:------:|:-----------:|
| [![Build status](https://api.travis-ci.com/fsquillace/junest.png?branch=master)](https://app.travis-ci.com/github/fsquillace/junest) [![OpenHub](https://www.openhub.net/p/junest/widgets/project_thin_badge.gif)](https://www.openhub.net/p/junest) | [![Github Sponsors](https://img.shields.io/badge/GitHub-Sponsors-orange.svg)](https://github.com/sponsors/fsquillace) [![PayPal](https://img.shields.io/badge/PayPal-Donation-blue.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=8LEHQKBCYTACY) | [![Join the gitter chat at https://gitter.im/fsquillace/junest](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/fsquillace/junest?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge) [![RSS](https://img.shields.io/badge/RSS-News-orange.svg)](http://fsquillace.github.io/junest-site/feed.xml) |

Description
===========
**JuNest** (Jailed User NEST) is a lightweight Arch Linux based distribution
that allows to have disposable and partial isolated GNU/Linux environments
within any generic GNU/Linux host OS
and without the need to have root privileges for installing packages.

JuNest contains mainly the package managers (called [pacman](https://wiki.archlinux.org/index.php/Pacman)
that allows to access
to a wide range of packages from the Arch Linux repositories.

The main advantages on using JuNest are:

- Install packages without root privileges.
- Partial isolated environment in which you can install packages without affecting a production system.
- Access to a wide range of packages, in particular on GNU/Linux distros that may contain limited repositories (such as CentOS and RedHat).
- Available for `x86_64` and `arm` architectures but you can build your own image from scratch too!
- Run on a different architecture from the host OS via QEMU
- All Arch Linux lovers can have their favourite distro everywhere!

JuNest follows the [Arch Linux philosophy](https://wiki.archlinux.org/index.php/The_Arch_Way).

How different is JuNest from Docker and Vagrant?
------------------------------------------------
Although JuNest sounds similar to a virtualisation/Linux container -like system,
JuNest is quite different from solutions like Docker or Vagrant.
In fact, the purpose of JuNest is **not** to
build a complete isolated environment but, conversely, is the ability to run
programs as they were running natively from the host OS. Almost everything is shared
between host OS and the JuNest sandbox (kernel, process subtree, network, mounting, etc)
and only the root filesystem gets isolated
(since the programs installed in JuNest need to reside elsewhere).

This allows interaction between processes belonging to both host OS and JuNest.
For instance, you can install `top` command in JuNest in order to monitor
any processes belonging to the host OS.

Blog posts [![RSS feed]({{site.baseurl}}/images/feed-icon-28x28.png)]({{site.baseurl}}/feed.xml "RSS feed") [![RSS feedly]({{site.baseurl}}/images/feedly-icon-28x28.png)](https://feedly.com/i/subscription/feed/{{site.url}}feed.xml "Feedly RSS")
==========
<ul class="posts">
  {% for post in site.posts %}
  <li>
    <span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{site.baseurl}}{{ post.url }}">{{post.title}}</a>
<!--The following looks not always working; keeping it commented for the moment-->
<!--(<a href="{{site.baseurl}}{{ post.url }}#disqus_thread" data-disqus-identifier="{{post.url}}"></a>)-->
  </li>
{% endfor %}
</ul>

{% include comment-counts.html %}
