---
layout: post

title: 计算数组中的最大值/最小值
tip-number: 45
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: 对于纯数字数组，使用内置函数Math.max()和Math.min()的方法。
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /zh_cn/calculate-the-max-min-value-from-an-array/

categories:
    - zh_CN
    - javascript
---

内置函数[Math.max()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/max)和[Math.min()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/min)可以分别找出参数中的最大值和最小值。

```js
Math.max(1, 2, 3, 4); // 4
Math.min(1, 2, 3, 4); // 1
```

这些函数对于数字组成的数组是不能用的。但是，这有一些类似地方法。

[`Function.prototype.apply()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)让你可以使用提供的`this`与参数组成的_数组(array)_来调用函数。

```js
var numbers = [1, 2, 3, 4];
Math.max.apply(null, numbers) // 4
Math.min.apply(null, numbers) // 1
```

给`apply()`第二个参数传递`numbers`数组，等于使用数组中的所有值作为函数的参数。

一个更简单的，基于ES2015的方法来实现此功能，是使用[展开运算符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_operator).

```js
var numbers = [1, 2, 3, 4];
Math.max(...numbers) // 4
Math.min(...numbers) // 1
```

此运算符使数组中的值在函数调用的位置展开。
