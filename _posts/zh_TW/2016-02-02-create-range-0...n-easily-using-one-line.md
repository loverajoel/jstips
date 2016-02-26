---
layout: post

title: 使用一行程式碼簡單建立一個 0...(N - 1) 的陣列
tip-number: 33
tip-username: SarjuHansaliya
tip-username-profile: https://github.com/SarjuHansaliya
tip-tldr: 我們透過一行程式碼簡單建立一個範圍函式，它可以給定一個 0...(N - 1) 的範圍。


categories:
    - zh_TW
---

使用下方的程式碼，我們可以建立一個 0...(N - 1) 的陣列。

```js
Array.apply(null, {length: N}).map(Number.call, Number);
```

讓我們來拆解這行程式碼。我們知道 `call` 函式可以在 JavaScript 執行，所以，在 `call` 第一個參數是上下文（context），而第二個參數開始則是呼叫 `call` 函式所需要用到的參數。

```js
function add(a, b){
    return (a + b);
}
add.call(null, 5, 6);
```
回傳 5 和 6 的總和。

在 JavaScript 陣列的 `map()` 帶有兩個參數，第一個是 `callback`，第二個則是 `thisArg(context)`。`callback` 中帶有三個參數，`value`、`index` 以及整個要被迭代的陣列。一般語法像是這樣：

```js
[1, 2, 3].map(function(value, index, arr){
    // 程式碼
}, this);
```
以下程式碼建立特定長度的陣列。

```js
Array.apply(null, {length: N})
```
把所有部分組合一起就是如下的解決方法。

```js
Array.apply(null, {length: N}).map(Number.call, Number);
```

如果你想要 1...N 的範圍，你可以像這樣。

```js
Array.apply(null, {length: N}).map(function(value, index){
  return index + 1;  
});
```
