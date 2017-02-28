---
layout: post

title: Calculate the Max/Min value from an array
tip-number: 45
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: Ways to use the built-in functions Math.max() and Math.min() with arrays of numbers
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /en/calculate-the-max-min-value-from-an-array/

categories:
    - en
    - javascript
---

The built-in functions [Math.max()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/max) and [Math.min()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/min) find the maximum and minimum value of the arguments, respectively.

```js
Math.max(1, 2, 3, 4); // 4
Math.min(1, 2, 3, 4); // 1
```

These functions will not work as-is with arrays of numbers. However, there are some ways around this.

[`Function.prototype.apply()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) allows you to call a function with a given `this` value and an _array_ of arguments.

```js
var numbers = [1, 2, 3, 4];
Math.max.apply(null, numbers) // 4
Math.min.apply(null, numbers) // 1
```

Passing the `numbers` array as the second argument of `apply()` results in the function being called with all values in the array as parameters.

A simpler, ES2015 way of accomplishing this is with the new [spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator).

```js
var numbers = [1, 2, 3, 4];
Math.max(...numbers) // 4
Math.min(...numbers) // 1
```

This operator causes the values in the array to be expanded, or "spread", into the function's arguments.
