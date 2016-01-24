---
layout: post

title: Rounding the fast way
tip-number: 18
tip-username: pklinger
tip-username-profile: https://github.com/pklinger
tip-tldr: Today's tip is about performance. Ever came across the double tilde `~~` operator? It is sometimes also called the double NOT bitwise operator. You can use it as a faster substitute for `Math.floor()`. Why is that?

categories:
    - en
---

Today's tip is about performance. [Ever came across the double tilde] (http://stackoverflow.com/questions/5971645/what-is-the-double-tilde-operator-in-javascript) `~~` operator? It is sometimes also called the double NOT bitwise operator. You can use it as a faster substitute for `Math.floor()`. Why is that?

One bitwise shift `~` transforms the 32 bit converted input into `-(input+1)`. The double bitwise shift therefore transforms the input into `-(-(input + 1)+1)` making it a great tool to round towards 0. For numeric input, it therefore mimics the `Math.ceil()` for negative and `Math.floor()` for positive input. On failure, `0` is returned, which might come in handy sometimes instead of `Math.floor()`, which returns a value of `NaN` on failure.

```javascript
// single ~
console.log(~1337)    // -1338

// numeric input
console.log(~~47.11)  // -> 47
console.log(~~-12.88) // -> -12
console.log(~~1.9999) // -> 1
console.log(~~3)      // -> 3

// on failure
console.log(~~[]) // -> 0
console.log(~~NaN)  // -> 0
console.log(~~null) // -> 0

// greater than 32 bit integer fails
console.log(~~(2147483647 + 1) === (2147483647 + 1)) // -> 0
```

Although `~~` may perform better, for the sake of readability please use `Math.floor()`.