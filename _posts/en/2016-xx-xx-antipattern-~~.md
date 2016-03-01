---
layout: *post

title: Antipattern: ~~
tip-number: xx
tip-username: gromgit
tip-username-profile: https://github.com/gromgit
tip-tldr: Don't say `~~` when you mean `Math.floor()`

categories:
    - en
---

### The Setup

The _double bitwise NOT_ is a fairly obscure trick. Among other things, it can function as a native operator replacement for `Math.floor()`:
```js
~~1234.567
==> 1234
```

### The Problem

First, it's a trick, so it often forces developers to stop and wonder if they've just introduced a logic bug.

More importantly, `~` [does something unexpected behind the scenes](https://es5.github.io/x11.html#x11.4.8):
> Let oldValue be **ToInt32**(GetValue(expr))

This means **_every float you `~~` turns into a 32-bit integer_**!  If, say, you use it to truncate the milliseconds portion of a Unix epoch timestamp, you've got a Y2038 problem:
```js
a = +new Date('2040-01-01') / 1000 + 0.123   // Unix epoch for 2040-01-01 00:00:00.123
==> 2208988800.123

~~a
==> -2085978496  // Oops
```

### The Solution

For clarity and correctness, **always** use `Math.floor()` when you mean `Math.floor()`:
```js
a = +new Date('2040-01-01') / 1000 + 0.123
==> 2208988800.123

Math.floor(a)
==> 2208988800
```
