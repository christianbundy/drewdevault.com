---
title: New sysadmin lecture
---

You're a production sysadmin now. That comes with certain responsibilities. In
short:

1. Respect the user's privacy, and look at only what you must.
2. Think before you type.
3. With great power comes great responsibility.

Assorted tips:

- Practice your changes on localhost first.
- Ask for help if you need it.
- Always run your SQL queries in a transaction.
- `SELECT things, you, want FROM x;` is generally better than `SELECT * FROM x;`
  when considering the user's privacy.
- Share information on a need-to-know basis, both with people and with
  computers.
- Avoid doing things that cannot be undone.

## Spear Phishing

Because you now have access to production systems, you may be a target for spear
phishing. A bad actor may target you directly in a social engineering attack in
an attempt to get you to leverage your access to mistakenly compromise the
system. For example, someone may impersonate another admin and ask you to add an
SSH key to a server. You need to be aware of this risk.

If you receive a request to leverage your access for any reason, double check
the veracity of the request. Is the person on IRC identified with NickServ for
the correct account? Is the email they sent DKIM signed and verified from the
right sender? If in doubt, ask for a secondary form of authentication, such as a
PGP challenge.

This also applies to normal requests from users - don't let someone impersonate
another user in an attempt to gain access to or manipulate their account. Be
especially careful with requests from users with 2FA enabled.
