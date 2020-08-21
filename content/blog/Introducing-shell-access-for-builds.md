---
date: 2019-08-19
layout: post
title: Shell access for builds.sr.ht CI
tags: ["announcement", "sourcehut"]
---

Have you ever found yourself staring at a failed CI build, wondering desperately
what happened? Or, have you ever needed a fresh machine on-demand to test out an
idea in? Have you been working on Linux, but need to test something on OpenBSD?
Starting this week, builds.sr.ht can help with all of these problems, because
you can now SSH into the build environment.

<small class="text-muted">
  If you didn't know, <a href="https://sourcehut.org">Sourcehut</a> is the 100%
  open/libre software forge for hackers, complete with git and Mercurial
  hosting, CI, mailing lists, and more - with no JavaScript. Try it out!
</small>

The next time your build fails on builds.sr.ht, you'll probably notice the
following message:

![Screenshot of builds.sr.ht showing a prompt to SSH into the failed build
VM and examine it](https://sr.ht/thL-.png)

After the build fails, we process everything normally - sending emails,
webhooks, and so on - but keep the VM booted for an additional 10 minutes. If
you do log in during this window, we keep the VM alive until you log out or
until your normal build time limit has elapsed. Once you've logged in, you get a
shell and can do anything you like, such as examining the build artifacts or
tweaking the source and trying again.

```
$ ssh -t builds@azusa.runners.sr.ht connect 81809
Connected to build job #81809 (failed):
https://builds.sr.ht/jobs/~sircmpwn/81809
Your VM will be terminated 4 hours from now, or when you log out.

bash-5.0 $
```

You can also connect to any build over SSH by adding `shell: true` to your build
manifest. When you do, the VM will be kept alive after all of the tasks have
finished (even if it doesn't fail) so you can SSH in. You can also SSH in before
the tasks have finished, and tail the output of the build in your terminal. An
example use case might be getting a fresh Alpine environment to test build your
package on:

<script
  id="asciicast-wnLYZwDuvkbIHwgTdmnqtQpXh"
  src="https://asciinema.org/a/pafXXANiWHY9MOH2yXdVHHJRd.js" async
></script>
<noscript><i>This article includes third-party JavaScript content from
asciinema.org, a free- and open-source platform that I trust.</i></noscript>

This was accomplished with a simple build manifest:

```
image: alpine/edge
shell: true
sources:
- https://git.alpinelinux.org/aports
tasks:
- "prep-abuild": |
    abuild-keygen -an
```

Since build manifests run normally in advance of your shell login, you can do
things like install your preferred editor and dotfiles, pull down your SSH keys
through [build
secrets](https://man.sr.ht/tutorials/builds.sr.ht/using-build-secrets.md), or
anything else you desire to set up a comfortable working environment.

Furthermore, by leveraging the [builds.sr.ht
API](https://man.sr.ht/builds.sr.ht/api.md), you can write scripts which take
advantage of the shell features. Need a NetBSD shell? With a little scripting
you can get something like this working:

<script
  id="asciicast-8etTNE7Ptgmu6hO3cVDlvrAal"
  src="https://asciinema.org/a/pafXXANiWHY9MOH2yXdVHHJRd.js" async
></script>

With experimental multiarch support being rolled out, soon you'll be just a few
keystrokes away from an ARM or PowerPC shell, too.

I want to expand more on SSH access in the future. Stay tuned and [let me
know](mailto:sir@cmpwn.com) if you have any cool ideas!
