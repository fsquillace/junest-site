---
title: JuNest Linux
layout: default
---

JuNest
======
The Arch Linux based distro that runs upon any Linux distros without root access.

{% include star-me.html %}

|Project Status|Donation|Communication|
|:------------:|:------:|:-----------:|
| [![Build status](https://api.travis-ci.org/fsquillace/junest.png?branch=master)](https://travis-ci.org/fsquillace/junest) [![OpenHub](https://www.openhub.net/p/junest/widgets/project_thin_badge.gif)](https://www.openhub.net/p/junest) | [![PayPal](https://img.shields.io/badge/PayPal-Donate%20a%20beer-blue.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=8LEHQKBCYTACY) | [![Join the gitter chat at https://gitter.im/fsquillace/junest](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/fsquillace/junest?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge) [![Join the IRC chat at https://webchat.freenode.net/?channels=junest](https://img.shields.io/badge/IRC-JuNest-yellow.svg)](https://webchat.freenode.net/?channels=junest) [![Join the group at https://groups.google.com/d/forum/junest](https://img.shields.io/badge/Google Groups-JuNest-red.svg)](https://groups.google.com/d/forum/junest) [![RSS](https://img.shields.io/badge/RSS-News-orange.svg)](http://fsquillace.github.io/junest-site/feed.xml) |

Description
===========
**JuNest** (Jailed User NEST) is a lightweight Arch Linux based distribution that allows to have
an isolated GNU/Linux environment inside any generic host GNU/Linux OS
and without the need to have root privileges for installing packages.

JuNest contains mainly the package managers (called [pacman](https://wiki.archlinux.org/index.php/Pacman) and [yaourt](https://wiki.archlinux.org/index.php/Yaourt)) that allows to access
to a wide range of packages from the Arch Linux repositories.

The main advantages on using JuNest are:

- Install packages without root privileges.
- Isolated environment in which you can install packages without affecting a production system.
- Access to a wide range of packages in particular on GNU/Linux distros that may contain limited repositories (such as CentOS and RedHat).
- Available for x86\_64, x86 and ARM architectures but you can build your own image from scratch too!
- Run on a different architecture from the host OS via QEMU
- All Arch Linux lovers can have their favourite distro everywhere!

JuNest follows the [Arch Linux philosophy](https://wiki.archlinux.org/index.php/The_Arch_Way).

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
