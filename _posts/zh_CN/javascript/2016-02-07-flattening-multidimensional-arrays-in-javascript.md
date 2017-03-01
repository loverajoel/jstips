---
layout: post

title: Javascript多维数组扁平化
tip-number: 38
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: 将多位数组转化为单一数组的三种不同方法。
tip-writer-support: https://www.coinbase.com/loverajoel


redirect_from:
  - /zh_cn/flattening-multidimensional-arrays-in-javascript/

categories:
    - zh_CN
    - javascript
---

下面是将多位数组转化为单一数组的三种不同方法。

对于此数组：

```js
var myArray = [[1, 2],[3, 4, 5], [6, 7, 8, 9]];
```

我们需要的结果是：

```js
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### 解决方案1：使用[`concat()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)和[`apply()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

```js
var myNewArray = [].concat.apply([], myArray);
// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### 解决方案2：使用[`reduce()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce#Flatten_an_array_of_arrays)

```js
var myNewArray = myArray.reduce(function(prev, curr) {
  return prev.concat(curr);
});
// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### 解决方案3：

```js
var myNewArray3 = [];
for (var i = 0; i < myArray.length; ++i) {
  for (var j = 0; j < myArray[i].length; ++j)
    myNewArray3.push(myArray[i][j]);
}
console.log(myNewArray3);
// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```
在[这里](https://jsbin.com/qeqicu/edit?js,console)看一下三种逻辑的实际作用。

### 方案四：使用 ES6 的[展开运算符](https://developer.mozilla.org/zh－CN/docs/Web/JavaScript/Reference/Operators/Spread_operator)

```js
var myNewArray4 = [].concat(...myArray);
console.log(myNewArray4);
// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

在[这里](https://jsbin.com/janana/edit?js,console) 查看这四种方法

对于无限嵌套的数组请使用 Lodash 的 [flattenDeep()](https://lodash.com/docs#flattenDeep)。

如果你担心性能问题的话，[这里](http://jsperf.com/flatten-an-array-loop-vs-reduce/6) 有一个测试让你确认他们是如何执行的。

对于较大的数组试一下Underscore的[flatten()](https://github.com/jashkenas/underscore/blob/master/underscore.js#L501).

如果你对性能好奇，[这里](http://jsperf.com/flatten-an-array-loop-vs-reduce/6)有一个测试。