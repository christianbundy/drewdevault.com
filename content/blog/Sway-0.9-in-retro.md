---
date: 2016-08-02
# vim: tw=80
# Commands used to generate these stats:
# LoC per author: git ls-tree -r -z --name-only HEAD -- */*.c | xargs -0 -n1 git blame --line-porcelain HEAD |grep  "^author "|sort|uniq -c|sort -nr
# Commits per author: git shortlog
title: Sway 0.9 & One year of Sway
layout: post
tags: [sway]
---

Today marks one year since the [initial
commit](https://github.com/SirCmpwn/sway/commit/6a33e1e3cddac31b762e4376e29c03ccf8f92107)
of Sway. Over the year since, we've written 1,823 commits by 54 authors,
totalling 16,601 lines of C (and 1,866 lines of header files). This was written
over the course of 515 pull requests and 300 issues. Today, most i3 features are
supported. In fact, as of last week, all of the features from the i3
configuration I used before I started working on Sway are now supported by Sway.
Today, Sway looks like this (click to expand):

[![](https://sr.ht/ICd5.png)](https://sr.ht/ICd5.png)

For those who are new to the project, [Sway](http://swaywm.org) is an
i3-compatible Wayland compositor. That is, your existing [i3](http://i3wm.org/)
configuration file will work as-is on Sway, and your keybindings and colors and
fonts and for_window rules and so on will all be the same. It's i3, but for
Wayland, plus it's got some bonus features. Here's a quick rundown of what's
happened since the [previous state of Sway](/2016/04/20/State-of-sway.html):

* Stacked & tabbed layouts
* Customizable input acceleration
* Mouse support for swaybar
* Experimental HiDPI support
* New features for swaylock and swaybg
* Support for more i3 IPC features
* Tracking of the workspace new windows should arrive on
* Improved compatibility with i3
* Many improvements to the documentation
* Hundreds of bug fixes and small improvements

Since the last State of Sway, we've also seen packages land in the official
repositories of Gentoo, OpenSUSE Tumbleweed, and NixOS (though the last group
warn me that it's experimental). And now for some updated stats. Here's the
breakdown of **lines of code per author** for the top ten authors (with the
change from the previous state of Sway in parens):

<table class="table">
    <tbody>
        <tr><td>4659 (+352)</td><td>Mikkel Oscar Lyderik</td></tr>
        <tr><td>3024 (-35)</td><td>Drew DeVault</td></tr>
        <tr><td>2232 (+53)</td><td>taiyu</td></tr>
        <tr><td>1786 (-40)</td><td>S. Christoffer Eliesen</td></tr>
        <tr><td>1090 (+1090)</td><td>Zandr Martin</td></tr>
        <tr><td>619 (-63)</td><td>Luminarys</td></tr>
        <tr><td>525 (-19)</td><td>Cole Mickens</td></tr>
        <tr><td>461 (-54)</td><td>minus</td></tr>
        <tr><td>365 (-20)</td><td>Christoph Gysin</td></tr>
        <tr><td>334 (-11)</td><td>Kevin Hamacher</td></tr>
    </tbody>
</table>

Notably, Zandr Martin has started regular contributions to Sway and brought
himself right up to 5th place in a short time, and while he's still learning C to
boot. Not included here are his recent forays into contributing to our
dependencies as well. Thanks man! This time around, I also lost a much more
respectable line count - only 35 compared to 457 from the last update.

Here's the total **number of commits per author** for each of the top ten
committers:

<table class="table">
    <tbody>
        <tr><td>842</td><td> Drew DeVault</td></tr>
        <tr><td>239</td><td> Mikkel Oscar Lyderik</td></tr>
        <tr><td>186</td><td> taiyu</td></tr>
        <tr><td>97</td><td> Luminarys</td></tr>
        <tr><td>91</td><td> S. Christoffer Eliesen</td></tr>
        <tr><td>58</td><td> Christoph Gysin</td></tr>
        <tr><td>48</td><td> Zandr Martin</td></tr>
        <tr><td>30</td><td> minus</td></tr>
        <tr><td>25</td><td> David Eklov</td></tr>
        <tr><td>24</td><td> Mykyta Holubakha</td></tr>
    </tbody>
</table>

Most of what I do for Sway personally is reviewing and merging pull requests.
Here's the same figures using **number of commits per author, excluding merge
commits**, which changes my stats considerably:

<table class="table">
    <tbody>
        <tr><td>383</td><td> Drew DeVault</td></tr>
        <tr><td>224</td><td> Mikkel Oscar Lyderik</td></tr>
        <tr><td>170</td><td> taiyu</td></tr>
        <tr><td>96</td><td> Luminarys</td></tr>
        <tr><td>91</td><td> S. Christoffer Eliesen</td></tr>
        <tr><td>58</td><td> Christoph Cysin</td></tr>
        <tr><td>38</td><td> Zandr Martin</td></tr>
        <tr><td>30</td><td> minus</td></tr>
        <tr><td>25</td><td> David Eklov</td></tr>
        <tr><td>24</td><td> Mykyta Holubakha</td></tr>
    </tbody>
</table>

These stats only cover the top ten in each, but there are more - check out the
[full list](https://github.com/SirCmpwn/sway/graphs/contributors).

Sway is still going very strong, and continues developing at a fast pace. I've
updated [the roadmap](http://swaywm.org/roadmap) with our plans for Sway 1.0.
You might notice a few features have been reprioritized here, which increases
the scope of Sway 1.0. It'll be worth it, though, to make sure we have a solid
1.0 release. Hopefully we'll see that and more within the year ahead!
