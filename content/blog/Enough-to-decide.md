---
date: 2019-09-08
layout: post
title: How I decide between many programming languages
tags: [languages]
---

I have a few old standards in my toolbelt that I find myself calling upon most
often, but I try to learn enough about many programming languages to reason
about whether or not they're suitable to any use-case I'm thinking about. The
best way is to learn by doing, so getting a general impression of the utility of
many languages helps equip you with the knowledge of whether or not they'd be
useful for a particular problem even if you don't know them yet.

Only included are languages which I feel knowledgable enough about to comment
on, there are many that aren't here and which I encourage you to research.

## C

Pros: good performance, access to low-level tooling, useful in systems
programming, statically typed, standardized and venerable, the lingua franca,
universal support on all platforms.[^1]

[^1]: Except one, and it can go suck an egg for all I care.

Cons: string munging, extensible programming, poor availability of ergonomic
libraries in certain domains, has footguns, some programmers in the wild think
the footguns are useful.

<style>
.bullshit {
    color: white;
    font-style: italic;
    font-weight: bold;
    text-shadow: -1px -1px 0 #000,
           1px -1px 0 #000, -1px 1px 0 #000, 1px 1px 0 #000;
}
</style>

## Go

Pros: fast, conservative, good package manager and a healthy ecosystem, standard
library is well designed, best in class for many problems, has a spec and
multiple useful implementations, easy interop with C.

Cons: the runtime is too complicated, no distinction between green threads and
real threads (meaning all programs deal with the problems of the latter).

## Rust

Pros: it's <em class="bullshit">SAFE</em>, useful for systems programming,
better than C++, ecosystem which is diverse but just short of the npm disease,
easy interop with C.

Cons: far too big, non-standardized, only one meaningful implementation.

## Python

Pros: easy and fast to get things done, diverse package ecosystem of reasonably
well designed packages, deeply extensible, useful for server-side web software.

Cons: bloated, poor performance, dynamically typed, cpython internals being
available to programmers has led to an implementation monoculture.

## JavaScript

*\* and all of its derivatives, which ultimately inherit its problems.*

Pros: functional but with an expressive and C-like syntax, ES6 improved on many
fronts, async/await/promises are well designed, no threading.

Cons: dynamic types, package ecosystem is a flaming pile, many JS programmers
aren't very good at it and they make ecosystem-defining libraries anyway, born
in web browsers and inherited their many flaws.

## Java

*\* and all of its derivatives, which ultimately inherit its problems.*

Pros: has had enough long-term investment to be well understood and reasonably
fast.

Cons: hella boilerplate, missing lots of useful things, package management, XML
is everywhere, not useful for low-level programming (this applies to all
Java-family languages).

## C#

Pros: less boilerplate than Java, reasonably healthy package ecosystem, good
access to low level tools for interop with C, async/await started here.

Cons: ecosystem is in turmoil because Microsoft cannot hold a singular vision,
they became open-source too late and screwed over Mono.

## Haskell

*\* and every other functional-oriented programming language in its class, such
as elixir, erlang, most lisps, even if they resent being lumped together*

Pros: it's <em class="bullshit">FUNCTIONAL</em>, reasonably fast, useful
when the answer to your problem is more important than the means by which you
find it, good for research-grade[^2] compilers.

Cons: it's <em class="bullshit">FUNCTIONAL</em>, somewhat inscrutable, awful
package management, does not fit well into its environment, written by people
who wish the world could be described with a pure function and design software
as if it could.

[^2]: but not production-grade.

## Perl

Pros: [entertaining][perl-configure], best in class at regexes/string munging,
useful for making hacky kludges when such solutions are appropriate.

[perl-configure]: https://github.com/Perl/perl5/blob/blead/Configure

Cons: inscrutable, too extensible, too much junk/jank.

## Lua

Pros: embeddable & easily plugged into its host, fairly simple, portable.

Cons: 1-based indexing is objectively bad, the upstream maintainers are kind of
doing their own thing and no one really likes it.

## POSIX Shell scripts

Pros: nothing can string together commands better, if you learn 90% of it then
you can make pretty nice and expressive programs with it for a certain class of
problem, standardized (I do not use bash).

Cons: most people learn only 10% of it and therefore make pretty bad and
unintuitive programs with it, not useful for most complex tasks.

---

Disclaimer: I don't like the rest of these programming languages and would not
use them to solve any problem. If you don't want your sacred cow gored, leave
here.

## C++

Pros: none

Cons: ill-defined, far too big, <em class="bullshit">
Object Oriented Programming</em>, loads of baggage, ecosystem that buys into
its crap, enjoyed by bad programmers.

## PHP

Pros: none

Cons: every PHP programmer is bad at programming, the language is designed to
accommodate them with convenient footguns (or faceguns) at every step, and the
ecosystem is accordingly bad. No, PHP7 doesn't fix this. Use a real programming
language, jerk.

## Ruby

Pros: It's both <em class="bullshit">ENTERPRISE</em> and <em
class="bullshit">HIP</em> at the same time, and therefore effective at herding a
group of junior to mid-level programmers in a certain direction, namely towards
your startup's exit.

Cons: bloated, awful performance, before Node.js took off this is what all of
those programmers used.

## Scala

Pros: more expressive than Java, useful for <em class="bullshit">Big
Data</em> problems.

Cons: Java derivative, type system requires a PhD to comprehend, too siloed from
Java, meaning it gets all of the disadvantages of being a Java ecosystem member
but few of the advantages. The type system is so needlessly complicated that it
basically cripples the language on its own merits alone.
