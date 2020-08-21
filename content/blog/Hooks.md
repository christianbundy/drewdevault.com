---
date: 2015-04-19
# vim: tw=80
title: Hooks - running stuff on Github hooks
layout: post
---

I found myself in need of a simple tool for deploying a project on every git
commit, but I didn't have a build server set up. This led to Hooks - a very
simple tool that allows you to run arbitrary commands when Github's hooks
execute.

The configuration is very simple. In `/etc/hooks.conf`, write:

    [truecraft]
    repository=SirCmpwn/TrueCraft
    branch=master
    command=systemctl restart hooks
    valid_ips=204.232.175.64/27,192.30.252.0/22,127.0.0.1

You may include any number of hooks. The `valid_ips` entry in that example
allows you to accept hooks from Github and from localhost. Then you run Hooks
itself, it will execute your command when you push a commit to your repository.

This allows you to do continuous deployment on the cheap and easy. I hope you
find it useful. [Hooks](https://github.com/SirCmpwn/hooks).
