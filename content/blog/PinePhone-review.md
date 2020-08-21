---
date: 2019-12-18
layout: post
title: PinePhone review
tags: [review, mobile]
---

**tl;dr**: Holy shit! This is the phone I have always wanted. I have never been
this excited about the mobile sector before. However: the software side is
totally absent &mdash; phone calls are very dubious, SMS is somewhat dubious,
LTE requires some hacks, and everything will have to be written from the ground
up.

I have a PinePhone developer edition model, which I paid for out of pocket[^1]
and which took an excruciatingly long time to arrive. When it finally arrived,
it came with no SIM or microSD card (expected), and the eMMC had some half-assed
version of Android on it which just boot looped without POSTing to anything
useful[^2]. This didn't bother me in the slightest &mdash; like any other
computer I've purchased, I planned on immediately flashing my own OS on it. My
Linux distribution of choice for it is
[postmarketOS](https://postmarketos.org/), which is basically the mobile OS I'd
build if I wanted to build a mobile OS.

[^1]: In other words, no one paid me to or even asked me to write this review.

[^2]: I understand that the final production run of the PinePhone is going to ship with postmarketOS or something.

Let me make this clear: **right now, there are very few people, perhaps only
dozens, for whom this phone is the right phone, given the current level of
software support**. I am not using it as my daily driver, and I won't for some
time. The only kind of person I would recommend this phone to is a developer who
believes in the phone and wants to help build the software necessary for it to
work.  However, it seems to me that all of the right people *are* working on the
software end of this phone &mdash; everyone I'd expect from the pmOS community,
from KDE, from the kernel hackers &mdash; this phone has an unprecedented level
of community support and the software *will* be written.

So, what's it actually like?

<details>
  <summary>Expand for a summary of the specs</summary>
  <p>
    The device is about
    <abbr title="The thickness of a GameBoy cartridge">1 cm thick</abbr>
    and weighs
    <abbr
      title="The weight of one GameBoy Color, with batteries, without cartridge"
    >188 grams</abbr>. The screen is about 16 cm tall, of which 1.5 cm is bezel,
    and <abbr
      title="About the width and height of a GameBoy color, plus 1 inch of height"
    >7.5 cm wide</abbr> (5 mm of bezel). The physical size and weight is very
    similar to my daily driver, a Samsung Galaxy J7 Refine. It has a USB-C port,
    which I understand can be reconfigured for DisplayPort, and a standard
    headphone jack and speakers, both of which sound fine in my experience. The
    screen is 720x1440, and looks about as nice as any other phone. It has
    front- and back-facing cameras, which I've yet to get working (I understand
    that someone has got them working at some point), plus a flash/lamp on the
    back, and an <abbr
      title="Note that the only values for R, G, and B that I've managed to get working are 0.0 and 1.0 each, for a total of 7 possible colors (including off)"
    >RGB LED</abbr> on the front.
  </p>
  <p>
    The eMMC is 16G and, side note, had <em>seventeen</em> partitions on it when
    I first got the phone. 2G of RAM, 4 cores. It's not very powerful, but in my
    experience it runs lightweight UIs (such as <a
    href="https://swaywm.org">sway</a>) just fine. With very little effort by
    way of power management, and with obvious power sinks left unfixed, the
    battery lasts about 5 hours.
  </p>
</details>

In short, I'm quite satisfied with it, but I've never had especially strenuous
demands of my phone. I haven't run any benchmarks on the GPU, but it seems
reasonably fast and the open-source Lima driver supports GLESv2. The modem is
supported by [Ofono](https://01.org/ofono), which is a telephony daemon based on
dbus &mdash; however, I understand that we can just open `/dev/ttyUSB1` and talk
to the modem ourselves, and I may just write a program that does this. Using
Ofono, I have successfully spun up LTE internet, sent and received SMS messages,
and placed and answered phone calls - though the last one without working
audio. A friend from KDE, Bhushan Shah, is working on this and rumor has it that
a call has successfully been placed. I have not had success with MMS, but I
think it's possible. WiFi works. All of this with zero blobs and a kernel which
is... admittedly, pretty heavily patched, but [open
source](https://gitlab.com/pine64-org/linux) and making its way upstream.[^3]

[^3]: The upstream kernel actually does work if you patch in the DTS, but WiFi doesn't work and it's not very stable.

Of course, no one wants to place phone calls by typing a lengthy command into
their terminal, but that these features can be done in an annoying way means
that it's feasible to write applications that do this in a convenient way. For
my part, I have been working on some components of a mobile-friendly Wayland
compositor, based on Sway, which I'm calling Sway Mobile for the time being. I'm
not sure if Sway will actually stick around once it becomes difficult to bend to
my will (it's designed for keyboard-driven operation, after all), but I'm
building mobile shell components which will translate nicely to any other
wlroots-based compositors.

The first of these is a simple app drawer, which I've dubbed
[casa](https://git.sr.ht/~sircmpwn/casa). I have a lot more stuff planned:

- A new bar/notification drawer/quick action thing
- A dialer & call manager, maybe integrated with gnome-contacts
- A telephony daemon which records incoming SMS messages and pulls up the call
  manager for incoming phone calls. Idea: write incoming SMS messages into a
  Maildir.
- A new touch-friendly Wayland lock screen
- An on-screen keyboard program

Here's a video showing casa in action:

<video
  src="https://yukari.sr.ht/casa.webm?cache-break"
  style="max-width: 50%; margin: 0 auto; display: block"
  autoplay loop muted >
  Your browser does not support webm playback. Please choose a browser which
  supports free and open standards.
</video>

The latest version has 4 columns and uses the space a bit better. Also, in the
course of this work I put together the
[fdicons](https://gitlab.freedesktop.org/ddevault/fdicons) library, which may be
useful to some.

I have all sorts of other small things to work on, like making audio behave
better and improving power management. I intend to contribute these tools to
postmarketOS upstream as a nice lightweight plug-and-play UI package you can
choose from when installing pmOS, either improving their existing
postmarketos-ui-sway meta-package or making something new.

In conclusion: I have been waiting for this phone for years and years and years.
I have been hoping that someone would make a phone whose hardware was compatible
with upstream Linux drivers, and could *theoretically* be used as a daily driver
if only the software were up to snuff. I wanted this because I knew that the
free software community was totally capable of building the software for such a
phone, if only the hardware existed. This is actually happening &mdash; all of
the free software people I would hope are working on the PinePhone, are working
on the PinePhone. And it's only $150! I could buy four of them for the price of
the typical smartphone! And I just might!
