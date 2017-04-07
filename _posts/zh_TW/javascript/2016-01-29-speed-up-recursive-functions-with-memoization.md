---
layout: post

title: 使用 memoization 加速遞迴
tip-number: 29
tip-username: hingsir
tip-username-profile: https://github.com/hingsir
tip-tldr: 大家對費式（Fibonacci）數列都很熟悉。我們可以在 20 秒內寫出以下的函式。它可以執行，但是效率不高。它做了大量的重複計算，我們可以快取先前的計算結果來加快計算速度。


redirect_from:
  - /zh_tw/speed-up-recursive-functions-with-memoization/

categories:
    - zh_TW
    - javascript
---

大家對費式（Fibonacci）數列都很熟悉。我們可以在 20 秒內寫出以下的函式。

```js
var fibonacci = function(n) {
    return n < 2 ? n : fibonacci(n - 1) + fibonacci(n - 2);
}
```
它可以執行，但是效率不高。它做了大量的重複計算，我們可以快取先前的計算結果來加快計算速度。

```js
const fibonacci = (function() {
  let cache = [0, 1]; // cache the value at the n index
  return function(n) {
    if (cache[n] === undefined) {
      for (let i = cache.length; i <= n; ++i) {
        cache[i] = cache[i - 1] + cache[i - 2];
      }
    }
    return cache[n];
  }
})()
```
也許，我們可以定義高階函式，來接受一個函式作為參數，並回傳一個函式回傳的暫存值。

```js
const memoize = function(func) {
    let cache = {};
    return function() {
        const key = JSON.stringify(Array.prototype.slice.call(arguments));
        return key in cache ? cache[key] : (cache[key] = func.apply(this, arguments));
    }
}
fibonacci = memoize(fibonacci);
```

這裡是 ES6 版本的 memoize 函式。

```js
const memoize = function(func) {
    const cache = {};
    return (...args) => {
        const key = JSON.stringify(args)
        return key in cache ? cache[key] : (cache[key] = func(...args));
    }
}
fibonacci = memoize(fibonacci);
```
我們可以將 `memoize()` 使用在其他地方
* GCD（最大公因數）

```js
const gcd = memoize(function(a, b) {
    let t;
    if (a < b) t = b, b = a, a = t;
    while (b != 0) t = b, b = a % b, a = t;
    return a;
});
gcd(27, 183); //=> 3
```
* 階乘計算

```js
var factorial = memoize(function(n) {
    return (n <= 1) ? 1 : n * factorial(n - 1);
})
factorial(5); //=> 120
```

學習更多關於 memoization：

- [Memoization - Wikipedia](https://en.wikipedia.org/wiki/Memoization)
- [Implementing Memoization in JavaScript](https://www.sitepoint.com/implementing-memoization-in-javascript/)
