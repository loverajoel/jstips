---
layout: post

title: ES6 的 var 和 let
tip-number: 59
tip-username: richzw
tip-username-profile: https://github.com/richzw
tip-tldr: 在這個 tip，我將介紹 var 和 let 他們之間不同的作用域。我應該使用 let 替代 var 嗎？讓我們來看一下吧！

redirect_from:
  - /zh_tw/keyword-var-vs-let/

categories:
    - zh_TW
    - javascript
---

### 概觀

- 透過 `var` 被定義的變數，它的作用域是在 function 或任何外部已經被宣告的 function，是全域的 。
- 透過 `let` 被定義的變數，它的作用域是在一個區塊（block）。

```js
function varvslet() {
  console.log(i); // i 是 undefined 的，因為 hositing
  // console.log(j); // ReferenceError: j 沒有被定義

  for( var i = 0; i < 3; i++ ) {
    console.log(i); // 0, 1, 2
  };

  console.log(i); // 3
  // console.log(j); // ReferenceError: j 沒有被定義

  for( let j = 0; j < 3; j++ ) {
    console.log(j);
  };

  console.log(i); // 3
  // console.log(j); // ReferenceError: j 沒有被定義
}
```

### 詳細的差別

- 變數 Hoisting

  `let` 不會被 hoist 到整個區塊的作用域。相較之下，`var` 可以被 hoist。

```js
{
  console.log(c); // undefined。因為 hoisting
  var c = 2;
}

{
  console.log(b); // ReferenceError: b 沒有被定義
  let b = 3;
}
```

- 在迴圈的 Closure

  `let` 在每次迴圈可以重新被 bind，確保它從先前結束的迴圈被重新賦值，所以在 closure 它被用來避免一些問題。

```js
for (var i = 0; i < 5; ++i) {
  setTimeout(function () {
    console.log(i); // 輸出 '5' 五次
  }, 100);  
}
```

  fter replacing `var` with `let`使用 `let` 替代 `var`

```js
// print 1, 2, 3, 4, 5
for (let i = 0; i < 5; ++i) {
  setTimeout(function () {
    console.log(i); // 輸出 0, 1, 2, 3, 4
  }, 100);  
}
```


### 我應該使用 `let` 替代 `var` 嗎？

> 不是的，`let` 是新的區塊作用域。語法強調在當 `var` 已經信號區塊作用域時，`let` 應該替代 `var` ，否則請不要單獨使用 `var`。`let` 改善了在 JS 作用域的選項，而不是取代。`var` 對於變數依然是有用的，可被用在整個 function 之中。

### `let` 兼容性

- 在 server 端，像是 Node.js，你現在可以安心的使用 `let`。

- 在 client 端，透過 transpiler（像是 [Traceur](https://github.com/google/traceur-compiler)），你可以安心的使用 `let` 語法。否則請在[這裡](http://caniuse.com/#search=let)確認你的瀏覽器是否支援。

### Playground
<div>
  <a class="jsbin-embed" href="http://jsbin.com/yumaye/embed?js,console">JS Bin on jsbin.com</a><script src="http://static.jsbin.com/js/embed.min.js?3.39.11"></script>
</div>

### 更多資訊

- [Let keyword vs var keyword](http://stackoverflow.com/questions/762011/let-keyword-vs-var-keyword)
- [For and against let](https://davidwalsh.name/for-and-against-let)
- [Explanation of `let` and block scoping with for loops](http://stackoverflow.com/questions/30899612/explanation-of-let-and-block-scoping-with-for-loops/30900289#30900289).
