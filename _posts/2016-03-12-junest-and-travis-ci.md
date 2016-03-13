---
title: JuNest and Travis CI
layout: default
---

{{page.title}}
==============

[Travis CI](https://travis-ci.org/) offers different solutions for the continuous
integration based on two different infrastructures. One of them is container based
and the other one is a standard vm based platform.
Both of them allows test environment suitable for most use cases.
There are few drawbacks though.
Generally the package version are quite old and on the container
based infrastructure is not allowed the use of `sudo` command to install packages.
The Container based infrastructure allows to have packages only
via a whitelisted repository containing a limited amount of packages.
<!--more-->

The combination Travis+JuNest offers a neat solution for having the most updated packages
available for a test environment that can suitable in most of the cases.

There is a new tutorial available explaining how JuNest can help on
running integration tests in a CI environment.
Check it out:
[How to use JuNest within Travis CI](https://github.com/fsquillace/junest/wiki/How-to-use-JuNest-within-Travis-CI)

{% include comments.html%}
