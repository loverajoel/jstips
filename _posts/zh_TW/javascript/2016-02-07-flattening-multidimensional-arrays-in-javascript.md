---
layout: post

title: 在 JavaScript 中將多維陣列扁平化
tip-number: 38
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: 三種不同的解決方法，將多維陣列合併為單一的陣列。
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - zh_tw/flattening-multidimensional-arrays-in-javascript/

categories:
    - zh_TW
    - javascript
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

### 方案四：使用 ES6 的[展開運算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)

```js
var myNewArray4 = [].concat(...myArray);
console.log(myNewArray4);
// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

在[這裡](https://jsbin.com/janana/edit?js,console) 查看這四個方法的

如果需要無限的巢狀陣列嘗試使用 Lodash 的 [flattenDeep()](https://lodash.com/docs#flattenDeep)。

如果你擔心效能問題的話，[這裡](http://jsperf.com/flatten-an-array-loop-vs-reduce/6) 有一個測試讓你來確認它們是如何執行的。

對於較大的巢狀陣列可以嘗試使用 Underscore 的 [flatten()](https://github.com/jashkenas/underscore/blob/master/underscore.js#L501)。

如果你好奇效能方面的表現, [這裡](http://jsperf.com/flatten-an-array-loop-vs-reduce/6)有相關的測試。
