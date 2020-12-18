---
title: godocs.io is now available
date: 2020-12-18
---

The inevitable forced migration to pkg.go.dev is shipping with known
regressions. It's rolling on out without fixing, for example, [a problem I
pointed out in June](https://github.com/golang/go/issues/38986). godoc.org uses
special meta tags[^1] which can link up a source path and line number with a URL
for a git host's source view. pkg.go.dev instead hardcodes a list of hosted git
forges. git.sr.ht is among them &mdash; getting it added was my introduction to
this mess &mdash; but *only* the hosted instance, and no third-party git.sr.ht
instances. hg.sr.ht is still missing, too. The Go team committed to not shipping
with regressions, but that was (predictably) false.

I have [previously written about][previous] the botched pkg.go.dev roll-out.
It's a microcosm of Google's toxic engineering culture, demonstrating how Google
engineers are out-of-touch with the values and needs of their community. It
initially shipped as a proprietary replacement, with no intention of making it
open source until the community demanded it, under the rationale that it wasn't
useful for intranets.[^2] They didn't take the opportunity to address any of the
flaws in godoc.org's design, and instead introduced regressions and made those
flaws even worse.

And it's shipping, in this state, in Q1 2021.

This pattern appears to be common to many Google affairs, because it's the
primary means by which Googlers get promoted.

[previous]: https://drewdevault.com/2020/08/01/pkg-go-dev-sucks.html

In light of this, [godocs.io](https://godocs.io) is now available, running the
last version of godoc.org that pre-dates pkg.go.dev. It is my intention to keep
this running indefinitely, and you're welcome to use it for your own purposes or
projects.

I haven't made any especially interesting changes, but the source code [is
available on git.sr.ht](https://git.sr.ht/~sircmpwn/gddo) &mdash; feel free to
send patches along to [sir@cmpwn.com](mailto:sir@cmpwn.com) if you want to
submit (minor) improvements or bugfixes. One change I will definitely have to
make is a new solution for full-text search (probably just Postgres), because I
don't want to use AppEngine. If anyone wants to help with this, I would
appreciate your patch.

[^1]: Which have problems of their own, which, when I raised them, where quickly dismissed by the Go team.
[^2]: "Useful for intranets" is obviously not the defining reason why FOSS projects are good.
