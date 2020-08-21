---
date: 2020-08-16
layout: post
title: Status update, August 2020
tags: ["status update"]
---

Greetings! Today is another rainy day here in Philadelphia, which rather sours
my plans of walking over to the nearby cafe to order some breakfast to-go. But I
am tired, and if I'm going to make it to the end of this blog post in one piece,
I'm gonna need a coffee. brb.

Hey, that was actually pretty refreshing. It's just drizzling, and the rain is
nice and cool. Alright, here goes! What's new? I'll leave the Wayland news for
[Simon Ser's blog](https://emersion.fr/blog) this month - he's been working on
some exciting stuff. The [BARE encoding](https://baremessages.org/) announced
last month has received some great feedback and refinements, and there are now
six projects providing BARE support for their author's favorite programming
language[^1]. There have also been some improvements to the Go implementation
which should help with some SourceHut plans later on.

[^1]: Or in some cases, the language the author is begrudgingly stuck with.

On the subject of SourceHut, I've focused mainly on infrastructure improvements
this month. There is a new server installed for hg.sr.ht, which will also be
useful as a testbed for additional ops work planned for future expansion.
Additionally, the PostgreSQL backup system has been overhauled and made more
resilient, both to data loss and to outages. A lot of other robustness
improvements have been made fleet-wide in monitoring. I'll be working on more
user-facing features again next month, but in the meanwhile, contributors like
наб have sent many patches in which I'll cover in detail in the coming "What's
cooking" post for [sourcehut.org](https://sourcehut.org/blog).

Otherwise, I've been taking it easy this month. I definitely haven't been
spending a lot of my time on a secret project, no sir. Thanks again for your
support! I'll see you next month.

<details>
<summary>?</summary>
<pre>
use io;
use io_uring = linux::io_uring;
use linux;
use strings;

export fn main void = {
	let uring = match (io_uring::init(256u32, 0u32)) {
		err: linux::error => {
			io::println("io_uring::init error:");
			io::println(linux::errstr(err));
			return;
		},
		u: io_uring::io_uring => u,
	};

	let buf: [8192]u8 = [0u8...];
	let text: nullable *str = null;
	let wait = 0u;
	let offs = 0z;
	let read: *io_uring::sqe = null: *io_uring::sqe,
		write: *io_uring::sqe = null: *io_uring::sqe;
	let eof = false;

	while (!eof) {
		read = io_uring::must_get_sqe(&uring);
		io_uring::prep_read(read, linux::STDIN_FILENO,
			&buf, len(buf): u32, offs);
		io_uring::sqe_set_user_data(read, &read);
		wait += 1u;

		let ev = match (io_uring::submit_and_wait(&uring, wait)) {
			err: linux::error => {
				io::println("io_uring::submit error:");
				io::println(linux::errstr(err));
				return;
			},
			ev: uint => ev,
		};

		wait -= ev;

		for (let i = 0; i < ev; i += 1) {
			let cqe = match (io_uring::get_cqe(&uring, 0u, 0u)) {
				err: linux::error => {
					io::println("io_uring::get_cqe error:");
					io::println(linux::errstr(err));
					return;
				},
				c: *io_uring::cqe => c,
			};

			if (io_uring::cqe_get_user_data(cqe) == &read) {
				if (text != null) {
					free(text);
				};

				if (cqe.res == 0) {
					eof = true;
					break;
				};

				text = strings::must_decode_utf8(buf[0..cqe.res]);
				io_uring::cqe_seen(&uring, cqe);

				write = io_uring::must_get_sqe(&uring);
				io_uring::prep_write(write, linux::STDOUT_FILENO,
					text: *char, len(text): u32, 0);
				io_uring::sqe_set_user_data(write, &write);
				wait += 1u;
				offs += cqe.res;
			} else if (io_uring::cqe_get_user_data(cqe) == &write) {
				assert(cqe.res > 0);
				io_uring::cqe_seen(&uring, cqe);
			} else {
				assert(false, "Unknown CQE user data");
			};
		};
	};

	io_uring::close(&uring);
};
</pre>

<details>
<summary>hmm?</summary>
<p>I might note that I wrote this program to test my io_uring wrapper; it's not
representative of how normal programs will do I/O in the future.</p>
</details>
</details>
