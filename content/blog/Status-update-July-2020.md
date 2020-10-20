---
date: 2020-07-15
layout: post
title: Status update, July 2020
tags: ["status update"]
---

Hello again! Another month of FOSS development behind us, and we're back again
to share the results. I took a week off at the end of June, so my progress this
month is somewhat less than usual. Regardless, I have some updates for you,
mainly in the domain of SourceHut work.

But before we get to that, let's go over this month's small victories. One was
the invention of the [BARE message format](https://baremessages.org), which I
wrote [a blog post about][bare post] if you want to learn more. Since that
article, five new implementations have appeared from various authors: Rust,
Python, JavaScript, D, and Zig.

[bare post]: https://drewdevault.com/2020/06/21/BARE-message-encoding.html

I also wrote a couple of not-blogposts for this site (drewdevault.com),
including a page [dispelling misconceptions about static linking][dynlib],
and a page (that I hope you'll contribute to!) with [videos of people editing
text][editing]. Just dropping a link here in case you missed them; they didn't
appear in RSS and aren't blog posts. To help find random stuff like that on this
site, I've also established a [misc page][misc].

[dynlib]: /dynlib
[editing]: /editing
[misc]: /misc

Okay, on to SourceHut. Perhaps the most exciting development is the addition of
[continuous integration to the mailing lists][lists CI]. I've been working
towards this for some time now, and it's the first of many features which are
now possible thanks to the addition of the project hub. I intend to complete
some follow-up work improving the CI feature further still in the coming weeks.
I'm also planning an upgrade for the hardware that runs hg.sr.ht during the same
timeframe.

[lists CI]: https://sourcehut.org/blog/2020-07-14-setting-up-ci-for-mailing-lists/

That's all the news I have for now, somewhat less than usual. Some time off was
much-needed, though. Thanks for your continued support, and I hope you continue
to enjoy using my software!

<details>
<summary>...</summary>
<pre>
$ cat main.$ext
use io;
use strings;
use sys;

export fn main void =
{
	for (let i = 0; sys::envp[i] != null; i += 1) {
		let s = strings::from_c(sys::envp[i]);
		io::println(s);
	};
};
$ $redacted run main.$ext
error: main.$ext:8:41: incorrect type (&char) for parameter 1 (&char)
		let s = strings::from_c(sys::envp[i]);
                                        ^--- here
$ vim main.$ext
$ cat main.$ext
use io;
use strings;
use sys;

export fn main void =
{
	for (let i = 0; sys::envp[i] != null; i += 1) {
		let s = strings::from_c(sys::envp[i]);
		io::println(s);
		free(s);
	};
};
$ $redacted run main.$ext
DISPLAY=:0
EDITOR=vim
# ...
</pre>
</details>
