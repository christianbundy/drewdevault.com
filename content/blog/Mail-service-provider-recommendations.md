---
date: 2020-06-19
layout: post
title: Email service provider recommendations
tags: [email]
---

Email is important to my daily workflow, and I've built many tools which
encourage productive use of it for software development. As such, I'm often
asked for advice on choosing a good email service provider. Personally, I run
my own mail servers, but about a year ago I signed up for and evaluated many
different service providers available today so that I could make informed
recommendations to people. Here are my top picks, as well as the criteria by
which they were evaluated.

Unfortunately, almost all mail providers fail to meet my criteria.  As such, I
can only recommend two: Migadu and mailbox.org.

# #1: Migadu

[Migadu](https://www.migadu.com/en/index.html) is my go-to recommendation
for a mail service provider.

**Advantages**

- Migadu is a small company with strong values and no outside capital (i.e.
  no profit-motivated external influence). Email support and a human being
  answers, and their leadership is accessible if you have questions or feedback.
- Their pricing is based on bandwidth usage, and does not rely on artificial
  scarcity like limited domain names or mailboxes.
- Has lots of features for your postmaster - you can treat it as a managed mail
  server for your organization.

**Disadvantages**

- They have suffered from some outages in the past. The global mail system is
  tolerant of such outages - you don't have to worry about messages being lost
  if they were sent during an outage. Still, being unable to access your mail is
  a problem.
- If you are on a trial account, they will put an advertisement into your email
  signature. I don't think that it's ever appropriate for a mail service
  provider to edit your outgoing emails for any reason, and certainly not to
  advertise.

Full disclosure: SourceHut and Migadu agreed to a consulting arrangement to
build their [new webmail system](https://git.sr.ht/~emersion/alps), which should
be going into production soon. However, I had evaluated and started recommending
Migadu prior to the start of this project, and I believe that Migadu fares well
under the criteria I give at the end of this post.

# #2: mailbox.org

[Mailbox.org](https://mailbox.org/en/) may be desirable if you wish to have a
more curated experience, and less hands-on access to postmaster-specific
features.

**Advantages**

- Excellent first-class support for PGP, and many other strong security and
  privacy features are available.
- Was able to speak to the CEO directly to discuss my concerns and feedback, and
  have my questions answered. Raised some bugs and they were fixed in short
  order.

**Disadvantages**

- The interface is a little bit too JavaScript heavy for my tastes, and suffer
  from some bugs and lack of polish.
- They are a German company serving mostly German customers - German text leaks
  into the UI and documentation in some places.
- Completing a Google captcha is required to sign up.

# Others

Evaluated but not recommended: disroot, fastmail, posteo.de, poste.io,
protonmail, tutanota, riseup, cock.li, teknik, runbox, megacorp mail (gmail,
outlook, etc).

# Criteria for a good mail service provider

The following criteria are objective and non-negotiable:

1. Support for open standards including IMAP and SMTP
2. Support for users who wish to bring their own domain

This is necessary to preserve the user's ownership of their data by making it
accessible over open and standardized protocols, and their right to move to
another service provider by not fixing their identity to a domain name
controlled by the email provider. It is for these reasons that Posteo,
ProtonMail, and Tutanota are not considered suitable.

The remaining criteria are subjective:

1. Is the business conducted ethically? Are their incentives aligned with their
   customers, or with their investors?
2. Is it sustainable? Can I expect them to be around in 10 years? 20? 30?
3. Do they make unfounded claims about security or privacy, or develop
   techniques which ultimately rely on trusting them instead of supporting or
   improving standards which rely on encryption?[^1]
4. If they make claims about privacy or security, do they explain the
   limitations and trade-offs, or do they let you believe it's infallible?
5. Do you trust them with your personal data? What if they're compelled by law
   enforcement? What is their government like?[^2]

Bonus points:

- What is their relationship with open source?
- Can I sign up without an existing email address? Is there a chicken and egg
  problem here?[^3]
- How well do they handle plaintext email? Do they meet the criteria for
  recommended clients at
  [useplaintext.email](https://useplaintext.email/#implementation-recommendations)?

If you represent a mail service provider which you believe meets this criteria,
please [send me an email](mailto:sir@cmpwn.com).

[^1]: This also rules out ProtonMail and Tutanota, doubly damning them, especially because it provides an excuse for skipping IMAP and SMTP, which conveniently enables vendor lock-in.
[^2]: This rules out Fastmail because of their government (Australlia)'s hostile and subversive laws regarding encryption.
[^3]: Alarmingly rare, this one. It seems to be either this, or a captcha like mailbox.org does. I would be interested in seeing the use of client-side proof of work, or requiring someone to enter their payment details and successfully complete a charge instead.
