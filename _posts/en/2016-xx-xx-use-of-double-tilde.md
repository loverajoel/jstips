---
layout: post

title: Use of Double Tilde(~~)
tip-number:
tip-username: SarjuHansaliya
tip-username-profile: https://github.com/SarjuHansaliya
tip-tldr: Here I have shown use of double tilde


categories:
    - en
---

We can use `~~(Double tilde)` sign to convert float/double number to the largest integer less than or equal to absolute of a given number.Here is the example.

```js
~~3.5     -> 3
~~3.9     -> 3
~~(-3.9)  -> -3
```

Don't confuse with `Math.floor` which used to convert float/double number to the largest integer less than or equal to a given number.

```js
Math.floor(3.4)  -> 3
Math.floor(3.9)  -> 3
Math.floor(-3.9) -> -4
```
So we can say for positive numbers `~~` is short hand for `Math.floor`.

Some Examples.

```js
~~10.5     -> 10
~~(-10.9)  -> -10
~~(true)   -> 1
~~(false)  -> 0
~~("true") -> 0
~~("false") -> 0
~~("any string") -> 0
```

Note : Don't mix `~~` with `~`(Bitwise Operator).
