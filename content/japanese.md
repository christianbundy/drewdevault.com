---
layout: page
title: Drew DeVault's Japanese Learning Resources
---

**Note**: this is a work in progress. I last updated this page on 2019-11-12. If
that was a while ago, feel free to ping me and ask me to write some more.

## Table of Contents

1. [Introduction](#introduction)
1. [Bootstrapping](#bootstrapping)
1. [Anki deck generators](#anki-deck-generators)
1. [Kanji study](#kanji-study)
1. [Vocabulary study](#vocabulary-study)
1. [Grammar study](#grammar-study)
1. [Reading practice](#reading-practice)
1. [Writing practice](#writing-practice)
1. [Listening practice](#listening-practice)
1. [Speaking practice](#speaking-practice)
1. [Conversation skills](#conversations-skills)
1. [List of resources](#list-of-resources)

## Introduction

I've been studying Japanese for a few years now, and while I still have a lot to
learn I feel comfortable having conversations in Japanese, without feeling like
the other participant is having to be concious of the complexity of their
language use. Accomplishing that had been my goal from the start; yours may be
different. What follows is what I believe is a reasonably good approach to
self-directed Japanese language study.

The most important thing to understand is that there is no magic bullet.
Duolingo, Rosetta stone, even attending a Japanese course at a local college -
none of these approaches alone is sufficient to master the language. Instead,
you need to identify the core skills a language learner needs to develop, and
focus on improving them individually. These focus areas are listed in the table
of contents:

- Kanji
- Vocabulary
- Grammar
- Reading
- Writing
- Speaking
- Listening
- Conversation
- Translation

You will visit and revisit these thousands of times over the course of your
studies, but they are listed roughly in the order in which you will first
encounter them, or at least in the order I approached them. And though they are
all interconnected, they each are completely discrete skills and must be given
your attention directly, lest the sum of your mastery suffer for your
inattention.

It sounds like a lot of work, but if you internalize these facts then you'll
find it much easier to approach the language than you otherwise might. Let's
say, for example, that you're finding your grammar skills falling behind, and
your listening skills are suffering because you haven't internalized the new
grammatical concepts, but you're fine when reading because you can take your
time. In a traditional classroom setting, you're going to be left behind as the
textbook and your peers plow forward with pre-defined allotments of time to each
of these focus areas.

However, if you study alone and you're cognisant of these independent areas of
study and the approaches to each that work best for you, you can identify the
areas in which you're weak, how they're affecting your growth in other areas,
and the right strategies for improvement. Boldly try new study strategies for
each of these areas, and boldly drop the approaches which aren't working for
you. By making it a personal journey rather than a cookie-cutter journey, you'll
learn the language much more easily.

Remember to keep your goals in mind, and set them in the first place. "I want to
learn Japanese" is too broad of a goal. "I want to have conversations with
Japanese friends", "I want to watch anime without subtitles", "I want to read
untranslated light novels" - these are much better goals. Adjust your learning
strategy towards your particular goals.

## Bootstrapping

There is a certain level of minimum competence you need to have in order to
utilize language learning tools effectively. You need to do these things first:

1. Learn how to read and pronounce [Hiragana](https://en.wikipedia.org/wiki/Hiragana)
   and [Katakana](https://en.wikipedia.org/wiki/Katakana)
2. Learn the 100 most common [kanji](https://en.wikipedia.org/wiki/Kanji)

TODO: Generate anki decks for these. If you're reading this TODO and feeling put
out, just search AnkiWeb for these and pick them out, it's not a big deal.

Learning the Japanese writing system, despite being the worst writing system
I've ever encountered, cannot be avoided. But, do not despair, you can learn the
basics in a few weeks of memorization, and that's enough to move on to bigger
things. Don't worry about being perfect at hiragana and katakana at first - if
you're feeling comfortable with most of them and unsure about just a few, you're
ready to move on and pick up the remainder on the fly.

Do not use romaji.

**Do not use romaji.**

You *must* learn the writing system.

In more general terms, it's important to devote similar amounts of time to each
area of study while you're early in your learning. Each of these focus areas
reinforces the other, and this is critical for fostering a cohesive
understanding of the fundamentals of the language early on.

Memorization is going to take up most of your time spent studying Japanese.
Thankfully, there's a great tool for helping you do this: Anki!

## Anki deck generators

[Anki](https://apps.ankiweb.net/) is an open source memorization tool which uses
spaced repetition to help you review things you aren't comfortable with, and
avoid wasting your time reviewing things you are comfortable with. There is a
free desktop application, a free Android app, and a paid iOS app which is worth
the price and then some[^1]. There's also a version that runs in your web
browser, and you can sync between all of them.

[^1]: I don't mean that the iOS one is better than any other. They're all worth the price and then some, but the non-iOS ones are free.

The Android app is the best one in my experience, because there's no better
time to memorize Japanese words than when you're sitting on the toilet. With
Anki, you can stop covering the Facebook app in fecal matter and learn Kanji
instead.[^2]

[^2]: I also find Anki useful on trains and cars, on my couch, in waiting rooms, and so on, but like, seriously, toilet time is a gravely unexploited resource for self-improvement. Everyone already uses their phones there anyway, don't pretend you don't.

Because both I'm a nerd and well enough into my Japanese studies to have a
pretty good idea of how all of this works, I've written some tools for
*generating* Anki decks. [You can get the source
here](https://git.sr.ht/~sircmpwn/ddevlang) and use it to generate custom Anki
decks catered to the specific thing you want to study, or you can download one
of the ones I've generated for you.

### Pre-fab decks

**Note**: these are experimental. YMMV.

I've prepared a number of decks using my tools that you can download and get
started with right away. Each deck was generated with linguistic terminology in
Japanese (e.g. "名詞" instead of "noun"), is limited to #common words, and is
ordered by word usage frequency. These are configurable options you can change
if you generate them yourself.

**General vocabulary**

- [All common vocabulary words](https://yukari.sr.ht/anki/common-vocab.apkg)
- Counters[^3]: [basic](https://yukari.sr.ht/anki/counter-vocab.apkg) (101 words), [comprehensive](https://yukari.sr.ht/anki/counter-vocab-full.apkg) (232 words)
- Linguistic vocab[^4]: [basic](https://yukari.sr.ht/anki/linguistic-vocab.apkg) (58 words), [comprehensive](https://yukari.sr.ht/anki/linguistic-vocab-full.apkg) (697 words)

[^3]: Japanese has lots of specific words and kanji for counting things. It's similar to English words like "three heads of lettuce", "two loaves of bread", "ten grains of rice". (thanks /u/martindholmes for the analogy)
[^4]: This is useful for being able to ask questions about the language, in the language. If you were worried about the pre-generated decks using Japanese linguistic terminology, this is the deck for you.

**Specialized vocabulary**

I generate these on an as-needed basis, as I personally want to study specific
kinds of vocabulary.

- [Astronomy vocabulary](https://yukari.sr.ht/anki/astronomy.apkg)
- [Computer vocabulary](https://yukari.sr.ht/anki/comp.apkg)
- [Music vocabulary](https://yukari.sr.ht/anki/music.apkg)

**JLPT vocabulary**

[JLPT](https://www.jlpt.jp/e/) is the standard Japanese language proficiency
test, often included in immigration and job requirements in Japan.

Each JLPT category in separate decks:

[JLPT N5 (easiest)](https://yukari.sr.ht/anki/JLPT-N5.apkg) &mdash;
[JLPT N4](https://yukari.sr.ht/anki/JLPT-N4.apkg) &mdash;
[JLPT N3](https://yukari.sr.ht/anki/JLPT-N3.apkg) &mdash;
[JLPT N2](https://yukari.sr.ht/anki/JLPT-N2.apkg) &mdash;
[JLPT N1 (hardest)](https://yukari.sr.ht/anki/JLPT-N1.apkg)

Cumulative decks, including vocab from each prior level:

[JLPT N4-N5](https://yukari.sr.ht/anki/JLPT-N4-5.apkg) &mdash;
[JLPT N3-N5](https://yukari.sr.ht/anki/JLPT-N3-5.apkg) &mdash;
[JLPT N2-N5](https://yukari.sr.ht/anki/JLPT-N2-5.apkg) &mdash;
[JLPT N1-N5](https://yukari.sr.ht/anki/JLPT-N1-5.apkg)

**Note**: these are generated by searching '#common' on jisho.org and filtering
to the JLPT categories you asked for. Don't blame me if you fail JLPT because
you used these. Caveat emptor.

## Kanji study

Kanji is a bitch. If it makes you feel better, though, it's difficult for native
Japanese speakers, too. In short, you have to learn thousands of discrete
characters, and multiple pronunciations of each, through rote memorization
alone, and alone your skills with kanji will only ever be tangentially
applicable to practical skills like reading or writing. With repeated study and
the application of a suitable amount of time, kanji can be conquered fairly
easily. The application of time is the hard part.

Personally, I found diminishing returns with studying kanji specifically after I
learned 300-400 of them. After that, I switched to studying vocabulary and
learning the kanji on the way. I suggest you take a similar approach if you want
to reach functional fluency faster, and study kanji in particular only if it
interests you. If you want to write Japanese by hand, you will have to study
kanji directly, but it's much easier to use an IME to type in Japanese on your
computer or phone if that's acceptable to you.

I suggest studying kanji in [RTK
order](https://git.sr.ht/~sircmpwn/ddevlang/tree/master/rtk.py), which organizes
them by complexity, teaching you the building blocks of more complex kanji
early on. On the subject of stroke order: learn it for your first 100
characters, to get a feel for the general logic behind it. Then stop, unless you
want to learn to write by hand. There are two useful Anki decks for Kanji study:

- [All Kanji in RTK order](https://ankiweb.net/shared/info/1862058740)
- [Writing practice deck](https://ankiweb.net/shared/info/1741808368)

## Vocabulary study

If you can read, write, and pronounce hiragana and katakana, and have learned to
recognize at least enough kanji to understand the basics of radicals and
pronunciation (that is, you know what 音読み, 訓読み, and 熟語 are), you should
start studying vocabulary. Pick up my [common vocab deck](#anki-deck-generators)
and get started. I also recommend the
[linguistic vocabulary](#anki-deck-generators) decks as well, so that you can
learn the vocab necessary to ask questions about the language, using the
language. Another good vocabulary deck is [this one for complementing the Tae
Kim vocab guide](https://ankiweb.net/shared/info/424465799), which I'll discuss
more in the next section.

It's important to integrate your vocabulary learning. Practice by talking to
yourself (or your cat) in Japanese, and reading Japanese materials, even if you
can't understand them - just look for words you recognize and see if you can
remember the pronunciation and meaning. Each of the skills I've separated here
are studied separately, but reinforce each other. Vocabulary boils down to rote
memorization, which is the most difficult kind of study, so it's especially
important to reinforce it with your other skills.

## Grammar study

[Tae Kim's grammar guide](http://www.guidetojapanese.org/learn/) is the single
best resource for studying Japanese grammar.

I highly recommend studying the [Tae Kim vocabulary flash
cards](https://ankiweb.net/shared/info/424465799) while you're working through
the guide. It's helpful to be able to read the example texts without having to
scroll back and forth between them and the cheat sheets in every article.

TODO: Expand on this section

## Reading practice

TODO

## Writing practice

TODO

## Listening practice

TODO

## Speaking practice

TODO

## Conversation skills

TODO

## List of resources

- [Jisho.org](https://jisho.org): best Japanese/English dictionary
- [Anki](https://apps.ankiweb.net/): open source memorization app
- [Tae Kim's free grammar guide](http://www.guidetojapanese.org/learn/grammar)
- [Italki](https://www.italki.com/): reasonably priced 1-on-1 video tutors
- [Japanese language learning games](https://crossword-solver.io/japanese-language-practice-games/), thanks Hailey!
- The "Read Real Japanese" books (thanks Dara!)
- There's others, probably

**TODO**

- Similar page on American Sign Language?
- Get better at Japanese Sign Language
- Get better at Mandarin
- Get better at Korean
- Get better at Spanish
- Make a conlang
