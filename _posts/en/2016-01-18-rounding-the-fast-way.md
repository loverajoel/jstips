---
layout: post

title: Truncating the fast way
tip-number: 18
tip-username: pklinger
tip-username-profile: https://github.com/pklinger
tip-tldr: `~~X == Math.trunc(X)`...in certain cases

categories:
    - en
---

Today's tip is about performance. Have you ever come across the [double tilde `~~` operator](http://stackoverflow.com/questions/5971645/what-is-the-double-tilde-operator-in-javascript)? It's also often called the _double bitwise NOT_ operator. You can use it as a faster substitute for `Math.trunc()`. Why is that?

One bitwise shift `~` first truncates `input` to 32 bits, then transforms it into `-(input+1)`. The double bitwise shift therefore transforms the input into `-(-(input + 1)+1)` making it a great tool to round towards zero. For numeric input, it therefore mimics `Math.trunc()`. On failure, `0` is returned, which might come in handy sometimes instead of `Math.trunc()`, which returns `NaN` on failure.

```js
// single ~
console.log(~1337)    // -1338

// numeric input
console.log(~~47.11)  // -> 47
console.log(~~1.9999) // -> 1
console.log(~~3)      // -> 3
```

Experienced programmers generally avoid using `~~`, but in the interest of full disclosure, here's a clinical view on this operator.

### INDICATIONS

##### When every CPU cycle counts
`~~` is probably faster than `Math.trunc()` across the board, though you can [test that assumption](https://jsperf.com/jsfvsbitnot/10) on whichever platforms matter to you. However, you'd generally have to perform millions of such operations to have any visible impact at run time.

##### When code clarity is not a concern
If you're deliberately trying to obfuscate your logic, or help your minifier/uglifier, this is a relatively cheap way to do it.

### CONTRAINDICATIONS

##### When round-to-zero is the _wrong_ thing to do
Depending on your requirements, other `Math.XXX()` functions should be used instead:
```js
console.log(~~-12.88)           // -> -12
console.log(Math.floor(-12.88)) // -> -13

console.log(12.88)              // ->  12
console.log(Math.round(12.88))  // ->  13
```
This can potentially lead to _fencepost_ (off-by-one) errors when transforming floats to array indices or related ordinal values. For instance, if you're "pigeonholing" numbers on a "nearest integer" basis, you should use `Math.round()` instead of `~~`, but programmer laziness and the impact of **_10 whole characters saved per use_** on human fingers often triumph over cold logic.

##### When dealing with large-magnitude numbers
Because `~` first does a 32-bit conversion, `~~` results in bogus values around &plusmn;2.15 billion. If you don't properly range-check your input, a user could trigger unexpected behavior when the transformed value ends up being a great distance from the original:
```js
a = 2147483647   // maximum positive 32-bit integer
console.log(~~a) // ->  2147483647 (ok)
a += 10000       // ->  2147493647 (ok)
console.log(~~a) // -> -2147483648 (huh?)
```
One scenario that's heavily impacted involves dealing with Unix epoch timestamps (measured in seconds from 1 Jan 1970 00:00:00 UTC). A quick way to get such values is:
```js
epoch_int = ~~(+new Date() / 1000)  // Date() epochs in milliseconds, so we scale accordingly
```
However, when dealing with timestamps after 19 Jan 2038 03:14:07 UTC (sometimes called the **Y2038 limit**), this breaks horribly:
```js
// epoch timestamp for 1 Jan 2040 00:00:00.123 UTC
epoch     = +new Date('2040-01-01') / 1000 + 0.123  // ->  2208988800.123

// back to the future!
epoch_int = ~~epoch                                 // -> -2085978496
console.log(new Date(epoch_int * 1000))             // ->  Wed Nov 25 1903 17:31:44 UTC

// that was fun, now let's get real
epoch_flr = Math.floor(epoch)                       // ->  2208988800
console.log(new Date(epoch_flr * 1000))             // ->  Sun Jan 01 2040 00:00:00 UTC
```

##### When the original input wasn't sanitized
Because `~~` transforms every non-number into `0`:
```js
console.log(~~[])   // -> 0
console.log(~~NaN)  // -> 0
console.log(~~null) // -> 0
```
some programmers treat it as alternative to proper input validation. However, this can lead to strange logic bugs down the line, since you're no longer distinguishing between invalid inputs and actual `0` values. This is therefore _not_ a recommended practice.

##### When so many people write about it incorrectly
Most people who write about _double bitwise NOT_ incorrectly equate it with `Math.floor()`.

Others are more careful to mention `Math.floor()` for positive inputs and `Math.ceil()` for negative ones, but that forces you to stop and think about the values you're dealing with. This defeats the purpose of `~~` as a handy no-gotchas shortcut.

### DOSAGE
Avoid where possible. Use sparingly otherwise.

### ADMINISTRATION
1. Apply cautiously.
2. Sanitize values before applying.
3. Carefully document relevant assumptions about the values being transformed.
4. Review code to deal with, at minimum:
   * logic bugs where invalid inputs are instead passed to other code modules as valid `0` values
   * range errors on transformed inputs
   * fencepost errors due to incorrect rounding direction
