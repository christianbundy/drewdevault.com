---
title: Embrace, extend, and finally extinguish - Microsoft plays their hand
date: 2020-08-27
---

GitHub took a note out of the Microsoft "<abbr title="Embrace, Extend,
Extinguish">EEE</abbr>" playbook when designing their git services. They
**embraced** git, and then rather than building an interface on top of email
&mdash; the collaboration mechanism that git was designed to use, and which is
still used for Linux kernel development[^1] &mdash; they built their "pull
requests" mechanism.

[^1]: And hundreds of other projects, including git itself.

They took terminology which already had meaning &mdash; "fork", meaning the
creation a separate governing body and development upstream for a codebase, a
rather large task; and "pull request", a git workflow which prepares an email
asking a receipient to pull a large branch of changes from a non-centralized
source &mdash; and replaced these decentralized, open systems with a completely
incompatible system designed to keep you on GitHub and to teach you to
collaborate using GitHub's proprietary tools. They **extended** git in a
proprietary way.

Microsoft knows a good deal when they see one, and picked up GitHub for a cool
$7,500,000,000, after they had already completed the two steps in Microsoft's
[anti-open-source playbook][0]. They joined the Linux Foundation in late 2016,
after Azure failed to win people back to Windows Server, admitting defeat while
simultaneously carving out a space from which they could project their interests
over the kernel.

[0]: https://en.wikipedia.org/wiki/Embrace,_extend,_and_extinguish

Today, I discovered this article, "[Relying on plain-text email is a
'barrier to entry' for kernel development, says Linux Foundation board
member][1]", a title which conveniently chooses to refer to Sarah Novotny by
her role as a Linux Foundation board member, rather than by her full title,
"Sarah Novotny, Microsoft employee, transitive owner of GitHub, and patroness
saint of conflicts of interests." Finally, they're playing the **extinguish**
card. Naturally, a representative of Microsoft, a company which has long waged
war against open source, and GitHub, a company which explicitly built an
incompatible proprietary system to extend git, would have an interest in
dismantling the distributed, open system that git was designed for.

[1]: https://www.theregister.com/2020/08/25/linux_kernel_email/

I represent [sourcehut](https://sourcehut.org), a GitHub competitor which does
what GitHub wouldn't &mdash; interoperate with open, distributed protocols, and
in the form of 100% free and open-source software. I agree that the UX of
email-driven development could be better! But instead of investing $7.5B into
throwing the baby out with the bathwater, we've [built interactive
tutorials][2], [designed better mailing lists][3], [built web interfaces for
patch submission][4], [implemented CI for emails][5] and [sent improvements to
git upstream][6]. I wrote [an entire mail client which makes it easier to use
these tools][7]. We're planning on web-based review interface, too. The result
is a UX which provides a similar experience to GitHub, but without disrupting
the established open ecosystem.

[2]: https://git-send-email.io/
[3]: https://lists.sr.ht/~emersion/mrsh-dev/patches/4728
[4]: https://sr.ht/_fUk.webm
[5]: https://sourcehut.org/blog/2020-07-14-setting-up-ci-for-mailing-lists/
[6]: https://github.com/git/git/commits?author=ddevault 
[7]: https://aerc-mail.org/

*This* is how you improve the ecosystem, Microsoft. Take notes. Stick with the
embrace, move your extending *upstream*, and forget about extinguish.
