---
layout: post

title: Javascript多维数组扁平化
tip-number: 38
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: 将多位数组转化为单一数组的三种不同方法。


categories:
    - zh_CN
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

对于无限嵌套的数组试一下Underscore的[flatten()](https://github.com/jashkenas/underscore/blob/master/underscore.js#L501).

如果你对性能好奇，[这里](http://jsperf.com/flatten-an-array-loop-vs-reduce/6)有一个测试。