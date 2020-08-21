---
date: 2020-01-04
layout: basic
title: Hello world
---

Let's say you ask your programming language to do the simplest possible task:
print out "hello world". Generally this takes two syscalls: write and exit.
The following assembly program is the ideal Linux x86_64 program for this
purpose. A perfect compiler would emit this hello world program for any
language.

```
bits 64
section .text
global _start
_start:
	mov rdx, len
	mov rsi, msg
	mov rdi, 1
	mov rax, 1
	syscall

	mov rdi, 0
	mov rax, 60
	syscall

section .rodata
msg: db "hello world", 10
len: equ $-msg
```

Most languages do a whole lot of other crap other than printing out "hello
world", even if that's all you asked for.

<table class="table table-bordered">
  <thead>
    <tr>
      <th>Test case</th>
      <th>Source</th>
      <th>Execution time</th>
      <th>Total syscalls</th>
      <th>Unique syscalls</th>
      <th>Size (KiB)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Assembly</strong> (x86_64)</td>
      <td>
        <a href="#tests">test.S</a>
      </td>
      <td>0.00s real</td>
      <td>2</td>
      <td>2</td>
      <td>8.6 KiB*</td>
    </tr>
    <tr>
      <td><strong>Zig</strong> (small)</td>
      <td>
        <a href="#testzig">test.zig</a>
      </td>
      <td>0.00s real</td>
      <td>2</td>
      <td>2</td>
      <td>10.3 KiB</td>
    </tr>
    <tr>
      <td><strong>Zig</strong> (safe)</td>
      <td>
        <a href="#testzig">test.zig</a>
      </td>
      <td>0.00s real</td>
      <td>3</td>
      <td>3</td>
      <td>11.3 KiB</td>
    </tr>
    <tr>
      <td><strong>C</strong> (musl, static)</td>
      <td>
        <a href="#testc">test.c</a>
      </td>
      <td>0.00s real</td>
      <td>5</td>
      <td>5</td>
      <td>95.9 KiB</td>
    </tr>
    <tr>
      <td><strong>C</strong> (musl, dynamic)</td>
      <td>
        <a href="#testc">test.c</a>
      </td>
      <td>0.00s real</td>
      <td>15</td>
      <td>9</td>
      <td>602 KiB</td>
    </tr>
    <tr>
      <td><strong>C</strong> (glibc, static*)</td>
      <td>
        <a href="#testc">test.c</a>
      </td>
      <td>0.00s real</td>
      <td>11</td>
      <td>9</td>
      <td>2295 KiB</td>
    </tr>
    <tr>
      <td><strong>C</strong> (glibc, dynamic)</td>
      <td>
        <a href="#testc">test.c</a>
      </td>
      <td>0.00s real</td>
      <td>65</td>
      <td>13</td>
      <td>2309 KiB</td>
    </tr>
    <tr>
      <td><strong>Rust</strong></td>
      <td>
        <a href="#testrs">test.rs</a>
      </td>
      <td>0.00s real</td>
      <td>123</td>
      <td>21</td>
      <td>244 KiB</td>
    </tr>
    <tr>
      <td><strong>Crystal</strong> (static)</td>
      <td>
        <a href="#testcr">test.cr</a>
      </td>
      <td>0.00s real</td>
      <td>144</td>
      <td>23</td>
      <td>935 KiB</td>
    </tr>
    <tr>
      <td><strong>Go</strong> (static w/o cgo)</td>
      <td>
        <a href="#testgo">test.go</a>
      </td>
      <td>0.00s real</td>
      <td>152</td>
      <td>17</td>
      <td>1661 KiB</td>
    </tr>
    <tr>
      <td><strong>D</strong> (dmd)</td>
      <td>
        <a href="#testd">test.d</a>
      </td>
      <td>0.00s real</td>
      <td>152</td>
      <td>20</td>
      <td>5542 KiB</td>
    </tr>
    <tr>
      <td><strong>D</strong> (ldc)</td>
      <td>
        <a href="#testd">test.d</a>
      </td>
      <td>0.00s real</td>
      <td>181</td>
      <td>21</td>
      <td>10305 KiB</td>
    </tr>
    <tr>
      <td><strong>Crystal</strong> (dynamic)</td>
      <td>
        <a href="#testcr">test.cr</a>
      </td>
      <td>0.00s real</td>
      <td>183</td>
      <td>25</td>
      <td>2601 KiB</td>
    </tr>
    <tr>
      <td><strong>Go</strong> (w/cgo)</td>
      <td>
        <a href="#testgo">test.go</a>
      </td>
      <td>0.00s real</td>
      <td>211</td>
      <td>22</td>
      <td>3937 KiB</td>
    </tr>
    <tr>
      <td><strong>Perl</strong></td>
      <td>
        <a href="#testpl">test.pl</a>
      </td>
      <td>0.00s real</td>
      <td>255</td>
      <td>25</td>
      <td>5640 KiB</td>
    </tr>
    <tr>
      <td><strong>Java</strong></td>
      <td>
        <a href="#testjava">Test.java</a>
      </td>
      <td>0.07s real</td>
      <td>226</td>
      <td>26</td>
      <td>15743 KiB</td>
    </tr>
    <tr>
      <td><strong>Node.js</strong></td>
      <td>
        <a href="#testjs">test.js</a>
      </td>
      <td>0.04s real</td>
      <td>673</td>
      <td>40</td>
      <td>36000 KiB</td>
    </tr>
    <tr>
      <td><strong>Python 3</strong> (PyPy)</td>
      <td>
        <a href="#testpy">test.py</a>
      </td>
      <td>0.68s real</td>
      <td>884</td>
      <td>32</td>
      <td>9909 KiB</td>
    </tr>
    <tr>
      <td><strong>Julia</strong></td>
      <td>
        <a href="#testjl">test.jl</a>
      </td>
      <td>0.12s real</td>
      <td>913</td>
      <td>41</td>
      <td>344563 KiB</td>
    </tr>
    <tr>
      <td><strong>Python 3</strong> (CPython)</td>
      <td>
        <a href="#testpy">test.py</a>
      </td>
      <td>0.02s real</td>
      <td>1200</td>
      <td>33</td>
      <td>15184 KiB</td>
    </tr>
    <tr>
      <td><strong>Ruby</strong></td>
      <td>
        <a href="#testrb">test.rb</a>
      </td>
      <td>0.04s real</td>
      <td>1401</td>
      <td>38</td>
      <td>1283 KiB</td>
    </tr>
  </tbody>
</table>

<div style="text-align: right">
  <small>* See notes for this test case</small>
</div>

This table is sorted so that the number of syscalls goes up, because I reckon
more syscalls is a decent metric for how much shit is happening that you didn't
ask for (i.e. `write("hello world\n"); exit(0)`). Languages with a JIT fare much
worse on this than compiled languages, but I have deliberately chosen not to
account for this.

These numbers are real. This is more complexity that someone has to debug, more
time your users are sitting there waiting for your program, less disk space
available for files which actually matter to the user.

### Environment

Tests were conducted on January 3rd, 2020.

- gcc 9.2.0
- glibc 2.30
- musl libc 1.1.24
- Linux 5.4.7 (Arch Linux)
- Linux 4.19.87 (vanilla, Alpine Linux) is used for musl libc tests
- Go 1.13.5
- Rustc 1.40.0
- Zig 0.5.0
- OpenJDK 11.0.5 JRE
- Crystal 0.31.1
- NodeJS 13.5.0
- Julia 1.3.1
- Python 3.8.1
- PyPy 7.3.0
- Ruby 2.6.4p114 (2019-10-01 rev 67812)
- dmd 1:2.089.0
- ldc 2:1.18.0
- Perl 5.30.1

For each language, I tried to write the program which would give the most
generous scores without raising eyebrows at a code review. The size of all
files which must be present at runtime (interpreters, stdlib, libraries, loader,
etc) are included. Binaries were stripped where appropriate.

This was not an objective test, this is just an approximation that I hope will
encourage readers to be more aware of the consequences of their abstractions,
and their exponential growth as more layers are added.

### test.S

```
bits 64
section .text
global _start
_start:
	mov rdx, len
	mov rsi, msg
	mov rdi, 1
	mov rax, 1
	syscall

	mov rdi, 0
	mov rax, 60
	syscall

section .rodata
msg: db "hello world", 10
len: equ $-msg
```

```
nasm -f elf64 test.S
gcc -o test -static -nostartfiles -nostdlib -nodefaultlibs
strip test: 8.6 KiB
```

**Notes**

- This program only works on x86_64 Linux.
- The size depends on how you measure it:<br />
  *Instructions + data alone*: 52 bytes<br />
  *Stripped ELF*: 8.6 KiB<br />
  *Manually minified ELF*: [142 bytes](http://timelessname.com/elfbin/)

### test.zig

```
const std = @import("std");

pub fn main() !void {
    const stdout = try std.io.getStdOut();
    try stdout.write("hello world\n");
}
```

```
# small
zig build-exe test.zig --release-small --strip
# safe
zig build-exe test.zig --release-safe --strip
```

**Notes**

- Written with the assistance of Andrew Kelly (maintainer of Zig)

### test.c

```
int puts(const char *s);

int main(int argc, char *argv[]) {
    puts("hello world");
    return 0;
}
```

```
# dynamic
gcc -O2 -o test test.c
strip test

# static
gcc -O2 -o test -static test.c
strip test
```

**Notes**

- glibc programs can never truly be statically linked. The size reflects this.

### test.rs

```
fn main() {
    println!("hello world");
}
```

```
rustc -C opt-levels=s test.rs
```

**Notes**

- The final binary is dynamically linked with glibc, which is included in the
  size.

### test.go

```
package main

import "os"

func main() {
    os.Stdout.Write([]byte("hello world\n"))
}
```

```
# dynamic
go build -o test test.go

# static w/o cgo
GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -o test -ldflags '-extldflags "-f no-PIC -static"' -buildmode pie -tags 'osusergo netgo static_build' test.go
```

Aside: it is getting way too goddamn difficult to build static Go binaries.

**Notes**

- The statically linked test was run on Alpine Linux with musl libc. It doesn't
  link to libc in theory, but hey.

### Test.java

```
public class Test {
    public static void main(String[] args) {
        System.out.println("hello world");
    }
}
```

```
javac Test.java
java Test
```

### test.cr

```
puts "hello world\n"
```

```
# Dynamic
crystal build -o test test.cr

# Static
crystal build --static -o test test.cr
```

**Notes**

- The Crystal tests were run on Alpine Linux with musl libc.

### test.js

```
console.log("hello world");
```

```
node test.js
```

### test.jl

```
println("hello world")
```

```
julia test.jl
```

**Notes**

- Julia numbers were provided by a third party

### test.py

```
print("hello world")
```

```
# cpython
python3 test.py
# pypy
pypy3 test.py
```

### test.pl

```
print "hello world\n"
```

```
perl test.pl
```

**Notes**

- Passing /dev/urandom into perl is equally likely to print "hello world"

### test.d

```
import std.stdio;
void main()
{
    writeln("hello world");
}
```

```
# dmd
dmd -O test.d
# ldc
ldc -O test.d
```

### test.rb

```
puts "hello world\n"
```

```
ruby test.rb
```
