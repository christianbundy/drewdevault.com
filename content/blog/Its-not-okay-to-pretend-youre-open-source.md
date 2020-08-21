---
date: 2018-10-30
title: It's not okay to pretend your software is open source
layout: page
tags: ["philosophy", "free software"]
---

Unfortunately, I find myself writing about the Commons Clause again. For those
not in the know, the Commons Clause is an addendum designed to be added to free
software licenses. The restrictions it imposes (you cannot sell the software)
makes the resulting franken-license nonfree. I'm not going to link to the
project which brought this subject back into the discussion - they don't deserve
the referral - but the continued proliferation of software using the Commons
Clause gives me reason to speak out against it some more.

One of my largest complaints with the Commons Clause is that it hijacks
language used by open source projects to proliferate nonfree software, and
encourages software using it to do the same. Instead of being a new software
license, it tries to stick itself onto other respected licences - often the
Apache 2.0 license. The name, "Commons Clause", is also disingenuous, hijacking
language used by respected entities like Creative Commons. In truth, the Commons
Clause serves to remove software from the commons[^anti]. Combining these
problems gives you language like "Apache+Commons Clause", which is easily
confused with [Apache Commons][apache-commons].

[^anti]: This is why I often refer to it as the "Anti-Commons Clause", though I felt that was a bit too Stallman-esque for this article.
[apache-commons]: http://commons.apache.org/

Projects using the Commons Clause have also been known to describe their license
as "permissive" or "open", some even calling their software "open source". This
is dishonest. FOSS refers to "free and open source software". The former, free
software, is defined by the [free software definition][fsd], published by
[GNU][gnu]. The latter, open source software, is defined by the [open source
definition][osd], published by the [OSI][osi]. Their definitions are very
similar, and nearly all FOSS licenses qualify under both definitions. These are
unambiguous, basic criteria which protects developers, contributors, and users
of free and open source software. These definitions are so basic, important and
well-respected that dismissing them is akin to dismissing climate change.

[fsd]: https://www.gnu.org/philosophy/free-sw.en.html
[gnu]: https://gnu.org
[osd]: https://opensource.org/osd
[osi]: https://opensource.org

Claiming your software is open source, permissively licensed, free software,
etc, when you use the Commons Clause, is *lying*. These lies are pervasive among
users of the Commons Clause. The page listing [Redis
Modules](https://redis.io/modules), for example, states that only software under
an OSI-approved license is listed. Six of the modules there are using nonfree
licenses, and antirez seems content to [ignore the problem][exhibit-a] until [we
forget about it][exhibit-b]. They're in for a long wait - we're not going to
forget about **shady, dishonest, and unethical companies like Redis Labs**.

[exhibit-a]: https://github.com/antirez/redis-doc/pull/984
[exhibit-b]: https://github.com/RedisLabsModules/RediSearch/issues/518

I don't use nonfree software[^beer], but I'm not going to sit here and tell you
not to make nonfree software. You have every right to license your work in any
way you choose. However, if you choose not to use a FOSS license, you need to
own up to it. Don't pretend that your software is something it's not. There are
many benefits to being a member of the free software community, but you are not
entitled to them if your software isn't. This behavior has to stop.

[^beer]: Free as in freedom, not as in free beer.

Finally, I have some praise to offer. [Dgraph](https://dgraph.io/) was briefly
licensed under Apache plus the Commons Clause, and had the sort of misleading
and false information this article decries on their marketing website, docs, and
so on. However, they've rolled it back, and Dgraph is now using the Apache 2.0
license with no modifications.  Thank you!
