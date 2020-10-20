---
# vim: tw=80
# Commands used to generate these stats:
# LoC per author: git ls-tree -r -z --name-only HEAD -- */*.c | xargs -0 -n1 git blame --line-porcelain HEAD |grep  "^author "|sort|uniq -c|sort -nr
# Commits per author: git shortlog
date: 2016-04-20
title: State of Sway - April 2016
layout: post
tags: [sway]
---

Since the previous [State of Sway](/2015/12/20/State-of-sway.html), we have
accomplished quite a bit. We are now shipping versioned releases of sway, which
include support for window borders, input device configuration, more new
features, and many bug fixes and stability improvements. I'm also happy to say
that Sway 0.5 has landed in the Arch Linux community repository and I'm starting
to hear rumors of it landing in other Linux distros as well. Here's a quick
rundown of what's happened in the past four months:

* Window borders work now
* Input devices are configurable
* swaybar is much more mature, including support for i3status and i3blocks
* swaylock has reached a similar level of maturity
* New `include` config command to include sub-configs
* We have a [default wallpaper](https://github.com/SirCmpwn/sway/blob/master/assets/Sway_Wallpaper_Blue_1920x1080.png) and a logo now
* musl libc support has been added
* More features of the i3 IPC protocol have been implemented
* 18 more i3 commands have been implemented
* Many improvements to documentation
* Hundreds of bug fixes and small improvements

I'm a particularly big fan of the new include command, which allows me to add
this to my config file:

    include ~/.config/sway/config.d/`hostname`/*

The net of this is that it includes a set of configs specific to each machine I
run Sway on, which each have a unique output device & input device configuration
and several other details, but I can include them all under
[version control](https://gogs.sr.ht/SirCmpwn/dotfiles) to keep my dotfiles
synced between computers.

Today, sway looks like this:

[![](https://sr.ht/me1j.png)](https://sr.ht/me1j.png)

We're now making our way towards Sway 1.0. I have put together a roadmap of the
things we have done and the things that remain to do for Sway 1.0, which is
available on the improved website [here](http://swaywm.org/roadmap). We are
still now moving forward on many of these features, including the most asked for
feature: the stacked & tabbed window layouts, which is under development from
Mikkel Oscar Lyderik. He's given me this screenshot to tease you with:

![](https://sr.ht/0CkR.png)

All of this is only possible thanks to the hard work of dozens of contributors.
Here's the breakdown of **lines of code per author** for the top ten authors
(with the difference from the previous State of Sway in parenthesis):

<table class="table">
    <tbody>
        <tr><td>4307 (+3180)</td><td>Mikkel Oscar Lyderik</td></tr>
        <tr><td>3059 (-457)</td><td>Drew DeVault</td></tr>
        <tr><td>2285 (+115)</td><td>taiyu</td></tr>
        <tr><td>1826 (+40)</td><td>S. Christoffer Eliesen</td></tr>
        <tr><td>682 (-38)</td><td>Luminarys</td></tr>
        <tr><td>544 (+544)</td><td>Cole Mickens</td></tr>
        <tr><td>515 (-19)</td><td>minus</td></tr>
        <tr><td>385 (+185)</td><td>Christoph Gysin</td></tr>
        <tr><td>345 (+266)</td><td>Kevin Hamacher</td></tr>
        <tr><td>166 (+45)</td><td>crondog</td></tr>
    </tbody>
</table>

Once again, I'm no longer the author of the most lines of code. Sway now
has a grand total of 15,422 lines of C and 2,787 lines of headers. Here's the
total **number of commits per author** for each of the top 10
committers:

<table class="table">
    <tbody>
        <tr><td>688</td><td> Drew DeVault</td></tr>
        <tr><td>212</td><td> Mikkel Oscar Lyderik</td></tr>
        <tr><td>191</td><td> taiyu</td></tr>
        <tr><td>109</td><td> S. Christoffer Eliesen</td></tr>
        <tr><td>97</td><td> Luminarys</td></tr>
        <tr><td>58</td><td> Christoph Gysin</td></tr>
        <tr><td>34</td><td> minus</td></tr>
        <tr><td>18</td><td> crondog</td></tr>
        <tr><td>13</td><td> Yacine Hmito</td></tr>
        <tr><td>12</td><td> progandy</td></tr>
    </tbody>
</table>

As the maintainer of sway, *a lot* of what I do is reviewing and merging
contributions from others. So these statistics change a bit if we use **number
of commits per author, excluding merge commits**:

<table class="table">
    <tbody>
        <tr><td>343</td><td> Drew DeVault</td></tr>
        <tr><td>201</td><td> Mikkel Oscar Lyderik</td></tr>
        <tr><td>175</td><td> taiyu</td></tr>
        <tr><td>109</td><td> S. Christoffer Eliesen</td></tr>
        <tr><td>96</td><td> Luminarys</td></tr>
        <tr><td>58</td><td> Christoph Gysin</td></tr>
        <tr><td>34</td><td> minus</td></tr>
        <tr><td>18</td><td> crondog</td></tr>
        <tr><td>13</td><td> Yacine Hmito</td></tr>
        <tr><td>12</td><td> progandy</td></tr>
    </tbody>
</table>

These stats only cover the top ten in each, but there are more - check out the
[full list](https://github.com/SirCmpwn/sway/graphs/contributors). Hopefully
next time I write a blog post like this, we'll be well into the lifetime of Sway
1.0!
