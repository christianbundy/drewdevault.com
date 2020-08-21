---
date: 2018-09-04
layout: post
title: Conservative web development
tags: ["philosophy", "web"]
---

Today I turned off my ad blocker, enabled JavaScript, opened my network monitor,
and clicked the first link on Hacker News - a New York Times article. It started
by downloading a megabyte of data as it rendered the page over the course of
eight full seconds. The page opens with an advertisement 281 pixels tall, placed
before even the title of the article. As I scrolled down, more and more requests
were made, downloading a total of 2.8 MB of data with 748 HTTP requests. An
article was weaved between a grand total of 1419 vertical pixels of ad space,
greater than the vertical resolution of my display. Another 153-pixel ad is
shown at the bottom, after the article. Four of the ads were identical.

I was reminded to subscribe three times, for $1/week (after one year this would
become $3.75/week). One of these reminders attached itself to the bottom of my
screen and followed along as a scrolled. If I scrolled up, it replaced this with
a larger banner, which showed me three other articles and an ad. I was asked for
my email address once, though I would have had to fill out a captcha to submit
it. I took out my phone and repeated the experiment. It took 15 seconds to load,
and I estimate the ads took up a vertical space equal to 4 times my phone's
vertical resolution, each ad alone taking up half of my screen.

The text of the article is a total of 9037 bytes, including the title, author,
and date. I downloaded the images relevant to the article, including the
1477x1082[^1] title image. Before I ran them through an optimizer, they weighed
260 KB; after, 236 KB (using only lossless optimizations). 8% of the total
download was dedicated to the content. 5 discrete external companies were
informed of my visit to the page and given the opportunity to run artibrary
JavaScript on it.

[^1]: Greater than the vertical resolution of my desktop display.

If these are the symptoms, what is the cure? My basic principles are these:

- Use no, or very little, JavaScript
- Use raster images sparingly, if at all, and optimize them
- Provide interactivity with forms and clever CSS
- Identify wasted bandwidth and CPU cycles and optimize them

I've been building [sr.ht](https://meta.sr.ht) with these principles in mind,
and I spent a few hours this optimizing it further. What do the results look
like? The heaviest page, [the marketing page](https://meta.sr.ht), today weighs
<strong class="text-info">110 KB</strong> with a cold cache, and <strong
class="text-danger">4.6 KB</strong> warm. [A similar page](https://github.com/)
on GitHub.com[^2] weighs <strong class="text-info">2900 KB</strong> cold,
<strong class="text-danger">19.4 KB</strong> warm. [A more typical
page][srht-main] on sr.ht weighs <strong class="text-info">56.8 KB</strong>
cold and <strong class="text-danger">31.9 KB</strong> warm, after <strong
class="text-warning">2</strong> HTTP requests; on GitHub [the same
page][github-main] is <strong class="text-info">781 KB</strong> cold and
<strong class="text-danger">57.4 KB</strong> warm, <strong
class="text-warning">118</strong> requests. This file is 29.1 KB.  The sr.ht
overhead is <strong class="text-info">27.6 KB</strong> cold and <strong
class="text-danger">2.7 KB</strong> warm. The GitHub overhead is respectively
<strong class="text-info">751.9 KB</strong> and <strong class="text-danger">28.2
KB</strong>. There's also a 174-pixel-tall ad on GitHub encouraging me to sign
up for an account, shown before any of the content.

[srht-main]: https://git.sr.ht/~sircmpwn/linux/tree/master/init/main.c
[github-main]: https://github.com/torvalds/linux/blob/master/init/main.c

[^2]: You may have to log out to see this.

To be fair, the GitHub page has more features. As far as I can tell, most of
these aren't implemented *in* the page, though, and are rather links to other
pages. Some of the features *in* the page include a dropdown for filtering
branches and tags, popups that show detail when you hover over an avatars, some
basic interactivity in the search, all things that I can't imagine taking up
much space. Does this justify an order of magnitude increase in resource usage?

Honestly, GitHub does a pretty good job overall. Compared to our New York Times
example, they're downright *great*. But they could be doing better, and so could
we all. You can build beautiful, interactive websites with HTML and CSS alone,
supported by a simple backend. Pushing the complexity of rendering your
single-page app into the frontend might save you miniscule amounts of
server-side performance, but you'd just be offloading the costs onto your
visitor's phone and sucking their battery dry.

There are easy changes you can make. Enable caching on your web server, with a
generous expiry. Use a hash of your resources in the URL so that you can bust
the cache when you need to. Enable gzip for text resources, and HTTP/2. Run your
images through an optimizer, odds are they can be losslessly compressed.  There
are harder changes, too. Design your website to be usable without JavaScript,
and use small amounts of it to enhance the experience - rather than to *be* the
experience. Use CSS cleverly to provide interactivity[^3]. Find ways to offload
work to the server where you can[^4]. Measure your pages to look for places to
improve. Challenge yourself to find the simplest way of building the features
you want.

[^3]: For example, check out how I implemented the collapsable message details on the [lists.sr.ht archives](https://lists.sr.ht/~sircmpwn/sr.ht-dev/%3C20180830183221.32377-1-hilobakho%40gmail.com%3E)
[^4]: I did this when I upgraded to Font Awesome 5 recently. They want you to include some JavaScript to make their SVG icons work, but instead I wrote a [dozen lines of Python](https://git.sr.ht/~sircmpwn/core.sr.ht/tree/srht/flask.py?id=70e75e96dc664a1b487ef02cb9936cb8f69105c0#n49) on the backend which gave me a macro to dump the desired SVG directly into the page.

And if anyone at Google is reading, you should try recommending these strategies
for speeding up pages instead of pushing self-serving faux standards like AMP.
