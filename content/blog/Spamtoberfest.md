---
title: Spamtoberfest
date: 2020-10-01
outputs: [html, gemtext]
---

As I've [written before][0], the best contributors to a FOSS project are
intrinsically motivated to solve problems in your software. This sort of
contribution is often fixing an important problem and places a smaller burden on
maintainers to spend their time working with the contributor. I've previously
contrasted this with the "I want to help out!" contributions, where a person
just has a vague desire to help out. Those contributions are, generally, less
valuable and place a greater burden on the maintainer. Now, DigitalOcean has
lowered the bar even further with Hacktoberfest.

*Disclaimer: I am the founder of a FOSS project hosting company similar to GitHub.*

[0]: https://drewdevault.com/2020/08/10/How-to-contribute-to-FOSS.html

As I write this, a Digital Ocean-sponsored and GitHub-enabled Distributed Denial
of Service (DDoS) attack is ongoing, wasting the time of thousands of free
software maintainers with an onslaught of meaningless spam. Bots are spamming
[tens of thousands][1] of pull requests like this:

[![Screenshot of a spam pull request on GitHub which adds garbage to the README.md file](https://l.sr.ht/71VU.png)](https://github.com/hundredrabbits/100r.co/pull/39/files)

[1]: https://github.com/search?q=amazing+project+is:pr&type=Issues

The official response from both Digital Ocean and GitHub appears to be passing
the buck.  Digital Ocean addresses spam in their FAQ, putting the burden of
dealing with it entirely on the maintainers:

> Spammy pull requests can be given a label that contains the word "invalid" or
> "spam" to discount them. Maintainers are faced with the majority of spam that
> occurs during Hacktoberfest, and we dislike spam just as much as you. If
> you're a maintainer, please label any spammy pull requests submitted to the
> repositories you maintain as "invalid" or "spam", and close them. Pull
> requests with this label won't count toward Hacktoberfest.

via [Hacktoberfest FAQ](https://hacktoberfest.digitalocean.com/details)

Here's GitHub's response:

> The content and activity you are reporting appears to be related to
> Hacktoberfest. Please keep in mind that GitHub Staff is not enforcing
> Hacktoberfest rules; we will, however, enforce our own Acceptable Use
> Policies. According to the Hacktoberfest FAQ... [same quote as given above]

via [@kyleknighted@twitter.com][2]

[2]: https://twitter.com/kyleknighted/status/1311685461828612097

So, according to these two companies, whose responsibility is it to deal with
the spam that *they've* created? The maintainers, of course! All for a T-Shirt.

Let's be honest. Hacktoberfest has never generated anything of value for open
source. It's a marketing stunt which sends a deluge of low-effort contributions
to maintainers, leaving them to clean up the spam. I've never been impressed
with Hacktoberfest contributions, even the ones which aren't obviously written
by a bot:

[![Screenshot of a pull request which needlessly comment a CSS file](https://l.sr.ht/F-sU.png)](https://github.com/whatwg/html/pull/5975/files)

This is what we get with corporate-sponsored "social coding", brought to you by
Digital Ocean and GitHub and McDonalds, home of the Big Mac&trade;. When you
build the Facebook of coding, you get the Facebook of coding. We don't need to
give away T-Shirts to incentivize drive-by drivel from randoms who will never
get any closer to open source than a +1/-1 README.md change.

What would *actually* benefit FOSS is to enable the strong mentorship necessary
raise a new generation of **software engineers** under the tutelage of
maintainers who can rely on a strong support system to do their work. Programs
like Google Summer of Code do this better. Programs where a marketing department
spends $5,000 on T-Shirts to flood maintainers with garbage and clothe people in
ads are doing the opposite: *hurting* open source.

[![Screenshot of a friend's notifications, 9 out of 11 of which are spam](https://l.sr.ht/KoFK.png)](https://l.sr.ht/KoFK.png)

Check out [@shitoberfest on Twitter](https://twitter.com/shitoberfest) for more
Hacktoberfest garbage.
