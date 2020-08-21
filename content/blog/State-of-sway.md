---
date: 2016-12-27
# vim: tw=80
# Commands used to generate these stats:
# LoC per author: git ls-tree -r -z --name-only HEAD -- */*.c | xargs -0 -n1 git blame --line-porcelain HEAD |grep  "^author "|sort|uniq -c|sort -nr
# Commits per author: git shortlog
title: State of Sway December 2016 - secure your Wayland desktop, get paid to work on Sway
layout: post
tags: [sway]
---

Earlier today I released [sway
0.11](https://github.com/SirCmpwn/sway/releases/tag/0.11), which (along with
lots of the usual new features and bug fixes) introduces support for security
policies that can help realize the promise of a secure Wayland desktop. We also
just started a bounty program that lets you sponsor the things you want done and
rewards contributors for working on them.

Today sway has 19,371 lines of C (and 3,761 lines of header files) written by 70
authors across 2,067 commits. These were written through 589 pull requests and
425 issues. Sway packages are available today in the official repos of Arch,
Gentoo, Fedora, NixOS, openSUSE, Void Linux, and more. Sway looks like this:

[![](https://sr.ht/ICd5.png)](https://sr.ht/ICd5.png)

Side note: please add pretty screenshots of sway to [this wiki
page](https://github.com/SirCmpwn/sway/wiki/Screenshots-of-Sway). Thanks!

For those who are new to the project, [Sway](http://swaywm.org) is an
i3-compatible Wayland compositor. That is, your existing [i3](http://i3wm.org/)
configuration file will work as-is on Sway, and your keybindings and colors and
fonts and for_window rules and so on will all be the same. It's i3, but for
Wayland, plus it's got some bonus features. Here's a quick rundown of what's
new since the [previous state of Sway](/2016/08/02/Sway-0.9-in-retro.html):

* Security policy configuration (man sway-security)
* FreeBSD support
* Initial support for HiDPI among sway clients (swaybar et al)
* Support for new i3 features
* Clicky title bars
* Lots of i3 compatability improvements
* Lots of documentation improvements
* Lots of bugfixes

Today it seems that most of the features sway needs are implemented. Work hasn't
slowed down - there's been lots of work fixing small bugs, improving
documentation, fixing subtle incompatabilities with i3, and so on. However, to
encourage the development of new features, I've officially put into action the
new bounty program today. Here's how it works - you can donate to the features
you want to see, and you can claim the donations by implementing the features
and sending a pull request. To date I've received about $200 in donations
towards sway, and I've matched that with a donation of my own to bring it up to
$400. I've distributed these donations into various buckets of features. Not
every feature is for sway - anything that improves the sway experience is
eligible for a bounty, and in fact over half of the initial bounties are for
features in other parts of the ecosystem. For details on the program, check out
[this link](https://github.com/SirCmpwn/sway/issues/986).

Here's the updated stats. First, **lines of code per author**:

<table class="table">
    <tbody>
        <tr><td>3799 (+775)</td><td>Drew DeVault</td></tr>
        <tr><td>3489 (-1170)</td><td>Mikkel Oscar Lyderik</td></tr>
        <tr><td>1705 (-527)</td><td>taiyu</td></tr>
        <tr><td>1236 (-550)</td><td>S. Christoffer Eliesen</td></tr>
        <tr><td>1160 (+70)</td><td>Zandr Martin</td></tr>
        <tr><td>449 (-12)</td><td>minus</td></tr>
        <tr><td>311 (-54)</td><td>Christoph Gysin</td></tr>
        <tr><td>285 (+285)</td><td>D.B</td></tr>
        <tr><td>247 (-87)</td><td>Kevin Hamacher</td></tr>
        <tr><td>227 (-298)</td><td>Cole Mickens</td></tr>
        <tr><td>219 (+219)</td><td>David Eklov</td></tr>
    </tbody>
</table>

Finally, I'm the top contributor! I haven't been on top for over a year. Lots of
the top contributors are slowly having their lines of code reduced as lots of
new contributors are coming in and displacing them with refactorings and bug
fixes.

Here's the total **number of commits per author** for each of the top ten
committers:

<table class="table">
    <tbody>
        <tr><td>1009</td><td> Drew DeVault</td></tr>
        <tr><td>245</td><td> Mikkel Oscar Lyderik</td></tr>
        <tr><td>153</td><td> taiyu</td></tr>
        <tr><td>97</td><td> Luminarys</td></tr>
        <tr><td>91</td><td> S. Christoffer Eliesen</td></tr>
        <tr><td>68</td><td> Zandr Martin</td></tr>
        <tr><td>58</td><td> Christoph Gysin</td></tr>
        <tr><td>45</td><td> D.B</td></tr>
        <tr><td>33</td><td> Taiyu</td></tr>
        <tr><td>32</td><td> minus</td></tr>
    </tbody>
</table>

Most of what I do for Sway personally is reviewing and merging pull requests.
Here's the same figures using **number of commits per author, excluding merge
commits**, which changes my stats considerably:

<table class="table">
    <tbody>
        <tr><td>479</td><td> Drew DeVault</td></tr>
        <tr><td>229</td><td> Mikkel Oscar Lyderik</td></tr>
        <tr><td>138</td><td> taiyu</td></tr>
        <tr><td>96</td><td> Luminarys</td></tr>
        <tr><td>91</td><td> S. Christoffer Eliesen</td></tr>
        <tr><td>58</td><td> Christoph Gysin</td></tr>
        <tr><td>56</td><td> Zandr Martin</td></tr>
        <tr><td>45</td><td> D.B</td></tr>
        <tr><td>32</td><td> Taiyu</td></tr>
        <tr><td>32</td><td> minus</td></tr>
    </tbody>
</table>

These stats only cover the top ten in each, but there are more - check out the
[full list](https://github.com/SirCmpwn/sway/graphs/contributors).

Here's looking forward to sway 1.0 in 2017!
