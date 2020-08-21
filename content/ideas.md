---
layout: page
title: List of ideas
---

This is a list of ideas that I don't have time to work on right now, but I might
work on later or contribute to if someone else started up the project.
Naturally, all of these assume that the result is based on free and open-source
software, uses open standards and protocols, leverages federation if
appropriate, etc. Shoot me a message on [Mastodon](https://cmpwn.com/@sir) if
you want to pick my brain on any of these ideas, or to let me know they exist.

A **social networking site** which is designed to enrich IRL relationships.
Your instance would probably be run by someone in your neighborhood, and if you
wanted to hang out it'd match you up with people with similar interests and help
you hang out together IRL, be it having drinks at a bar or playing video games
or board games for an evening, or whatever else. Instead of "social networking"
sites which try to keep you stuck staring at their pages for as long as
possible, the prime directive of this site would be to quickly get you off of
your phone and into IRL face-time with other people.

A marriage of **git and bittorrent**, for the purpose of tracking large blobs.
Like git-lfs, but decentralized. Instead of storing the URL to fetch files from
like git-lfs does, it stores the infohash. git push should block until 100% of
the changes are replicated in the swarm.

A **vector graphics display** with open hardware, an open standard for driving
it from a PC, and upstream kernel drivers implementing that interface. Could be
CRT-style or a laser+mirror+projector kind of system, or both. Kernel interface
should be fairly general to encourage manufacturers to write drivers for it, and
should be paired with a nice userspace library for driving the ioctls, like DRM
but for vector graphics. Relevant resources:
[Hackaday](https://hackaday.com/2011/11/10/rgb-laser-projector-is-a-jaw-dropping-build/),
[Arduino RTOS](https://github.com/greiman/ChRt).

A **Wayland port of xscreensaver** based on layer-shell.

A **web browser engine** which flagrantly disregards modern web standards,
written in C or Rust. No JavaScript, limited CSS. Designed as a library which
others can make GUIs et al out of. Like Servo if they gave a shit about making
anything other than a testbed for rewriting Firefox.

A new **kernel for z80 calculators**. [KnightOS](https://knightos.org) is far
from the mark in terms of POSIX support and general Unixisms, but it'd probably
be a good start. There's no reason a POSIX-compatible operating system wouldn't
work on these devices. Particularly egregious failures in KnightOS include the
file descriptor design and the lack of a TTY subsystem, though depending on who
you ask that last one isn't so bad.

A simple replacement for **gas/nasm and binutils**, with less GNU and more
modularity. Ideally should pair well with
[cproc](https://git.sr.ht/~mcf/cproc)/qbe.

An **ethical engineering index** which defines a set of criteria by which tech
companies are evaluated for ethics and assigns each a score. Factors include
their approach to military contracting, their treatment of their employees,
attitude towards open source, etc. Above a certain rating, companies would be
allowed to post job listings for free (under that level they wouldn't be allowed
to post at all). There's no business model here, ping me for free hosting.
