---
date: 2016-08-18
# vim: tw=80
title: '[VIDEO] Arch Linux with full disk encryption in (about) 15 minutes'
layout: post
tags: [video, linux, encryption]
---

<link rel="stylesheet" href="/css/video-js.css">
<script>
window.HELP_IMPROVE_VIDEOJS = false;
</script>
<script src="/js/video.js"></script>

After my [blog post](/2016/06/29/Privacy-as-a-hobby.html) emphasizing the
importance of taking control of your privacy, I've decided to make a few more
posts going over detailed instructions on how to actually do so. Today we have a
video that goes over the process of installing Arch Linux with full disk
encryption.

This is my first go at publishing videos on my blog, so please provide some
feedback in the comments of this article. I'd prefer to use my blog instead of
YouTube for publishing technical videos, since it's all open source, ad-free,
and DRM-free. Let me know if you'd like to see more content like this on my
blog and which topics you'd like covered - I intend to at least release another
video going over this process for Ubuntu as well.

<video class="video-js vjs-16-9" data-setup="{}" controls>
  <source src="https://sr.ht/archlinux.webm" type="video/webm">
  <p>Your browser does not support HTML5 video.</p>
</video>

<a class="pull-right" href="https://sr.ht/archlinux.webm">Download video (WEBM)</a>

<div class="clearfix"></div>

The video goes into detail on each of these steps, but here's the high level
overview of how to do this. Always check the latest version of the [Install
Guide](https://wiki.archlinux.org/index.php/Installation_guide) and the
[dm-crypt](https://wiki.archlinux.org/index.php/Dm-crypt) page on the Arch Wiki
for the latest procedure.

1. Partition your disks with gdisk and be sure to set aside a partition for
   /boot
1. Create a filesystem on /boot
1. (optional) Securely erase all of the existing data on your disks with `dd
   if=/dev/zero of=/dev/sdXY bs=4096` - *note: this is a correction from the
   command mentioned in the video*
1. Set up encryption for your encrypted partitions with `cryptsetup luksFormat
   /dev/sdXX`
1. Open the encrypted volumes with `cryptsetup open /dev/sdXX [name]`
1. Create filesystems on /dev/mapper/[names]
1. Mount all of the filesystems on /mnt
1. Perform the base install with `pacstrap /mnt base [extra packages...]`
1. `genfstab -p /mnt >> /mnt/etc/fstab`
1. `arch-chroot /mnt /usr/bin/bash`
1. `ln -s /usr/share/zoneinfo/[region]/[zone] /etc/localtime`
1. `hwclock --systohc --utc`
1. Edit /etc/locale.gen to your liking and run `locale-gen`
1. `locale > /etc/locale.conf` - note this only works for en_US users, adjust if
   necessary
1. Edit /etc/hostname to your liking
1. Reconfigure the network
1. Edit /etc/mkinitcpio.conf and ensure that the `keyboard` and `encrypt` hooks
   run before the `filesystems` hook
1. `mkinitcpio -p linux`
1. Set the root password with `passwd`
1. Configure /etc/crypttab with any non-root encrypted disks you need. You can
   get partition UUIDs with `ls -l /dev/disk/by-partuuid`
1. Configure your kernel command line to include
   `cryptdevice=PARTUUID=[...]:[name] root=/dev/mapper/[name] rw`
1. Install your bootloader and reboot!
