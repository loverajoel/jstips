---
layout: post

title: 在 JavaScript 中扁平化多維陣列
tip-number: 38
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: 三種不同的解決方法，將多維陣列合併為單一的陣列。


categories:
    - zh_TW
---

三種不同的解決方法，將多維陣列合併為單一的陣列。

給定一個陣列：

```js
var myArray = [[1, 2],[3, 4, 5], [6, 7, 8, 9]];
```

我們想到得到這個結果：

```js
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### 方案一: 使用 [`concat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) 和 [`apply()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

```js
var myNewArray = [].concat.apply([], myArray);
// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### 方案二：使用 [`reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce#Flatten_an_array_of_arrays)

```js
var myNewArray = myArray.reduce(function(prev, curr) {
  return prev.concat(curr);
});
// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### 方案三：

```js
var myNewArray3 = [];
for (var i = 0; i < myArray.length; ++i) {
  for (var j = 0; j < myArray[i].length; ++j)
    myNewArray3.push(myArray[i][j]);
}
console.log(myNewArray3);
// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```
在[這裡](https://jsbin.com/qeqicu/edit?js,console)觀察三種方式的實際應用。

對於無限嵌套陣列嘗試一下 Underscore 的 [flatten()](https://github.com/jashkenas/underscore/blob/master/underscore.js#L501)。

如果你好奇效能方面表現, [這裡](http://jsperf.com/flatten-an-array-loop-vs-reduce/6)有相關的測試。
