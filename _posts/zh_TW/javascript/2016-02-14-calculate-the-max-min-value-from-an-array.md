---
layout: post

title: 從陣列計算最大和最小值
tip-number: 45
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: 在數字陣列使用內建的 Max.max() 和 Max.min() 函式的方式。
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /zh_tw/calculate-the-max-min-value-from-an-array/

categories:
    - zh_TW
    - javascript
---

內建函式 [Math.max()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/max) 和 [Math.min()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/min) 分別可以從參數中找到最大值和最小值。

```js
Math.max(1, 2, 3, 4); // 4
Math.min(1, 2, 3, 4); // 1
```

這些函式對於數字陣列是無法作用的。然而，這裡有些解決辦法。

[`Function.prototype.apply()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) 允許你呼叫函式並給定一個 `this` 和一個_陣列_的參數。

```js
var numbers = [1, 2, 3, 4];
Math.max.apply(null, numbers) // 4
Math.min.apply(null, numbers) // 1
```

傳送 `numbers` 陣列當作 `apply()` 的第二個參數，函式會呼叫陣列內所有的值當作函式的參數。

更簡單的方式，透過 ES2015 的[展開運算子](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)來完成。

```js
var numbers = [1, 2, 3, 4];
Math.max(...numbers) // 4
Math.min(...numbers) // 1
```

這個運算子可以在函式的參數中把陣列內的數值「展開」。
