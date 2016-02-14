---
layout: post

title: Calculate the Max/Min value from an array
tip-number: 45
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: There are two methods to find Max and Min numbers from an argument list of numbers but they doesn't support Arrays natively.

categories:
    - en
---

There are two methods to find Max and Min numbers from an argument list of numbers but they does not support Arrays natively.

```js
Math.max(1, 2, 3, 4); // 4
Math.min(1, 2, 3, 4); // 1
```

`apply()` allows you to use built-ins functions to find [Max](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/max) [Min](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/min) value in an `Array`.

```js
var numbers = [1, 2, 3, 4];
Math.max.apply(null, numbers) // 4
Math.min.apply(null, numbers) // 1
```

*The first arguent proveded to `apply()` is the context. In this case doesn't matter, but you can read more [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)*

Another way more easier is with the new [spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator).

```js
var numbers = [1, 2, 3, 4];
Math.max(numbers...) // 4
Math.min(numbers...) // 1
```

