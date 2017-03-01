---
layout: post

title: var和ES6的let
tip-number: 59
tip-username: richzw
tip-username-profile: https://github.com/richzw
tip-tldr: 在这个 tip，我将介绍 var 和 let 之间不同的作用域。我应该使用 let 替代 var 吗？让我们来看一下吧！
redirect_from:
  - /zh_cn/keyword-var-vs-let/

categories:
    - zh_CN
    - javascript
---

### 概述

- 通过 `var` 定义的变量，它的作用域是在 function 或任何外部已经被声明的 function，是全域的 。
- 透過 `let` 定义的变量，它的作用域是在一個块（block）。

```js
function varvslet() {
  console.log(i); // i 是 undefined 的，因为变量提升
  // console.log(j); // ReferenceError: j 没有被定义

  for( var i = 0; i < 3; i++ ) {
    console.log(i); // 0, 1, 2
  };

  console.log(i); // 3
  // console.log(j); // ReferenceError: j 没有被定义

  for( let j = 0; j < 3; j++ ) {
    console.log(j);
  };

  console.log(i); // 3
  // console.log(j); // ReferenceError: j 没有被定义
}
```

### 详细的区别

- 变量提升

  `let` 不會被提升到整个块的作用域。相比之下，`var` 可以被提升。

```js
{
  console.log(c); // undefined。因为变量提升
  var c = 2;
}

{
  console.log(b); // ReferenceError: b 没有被定义
  let b = 3;
}
```

- 循环中的闭包

  `let` 在每次循环可以重新被 bind，确保在它之前结束的循环被重新赋值，所以在闭包中它被用來避免一些问题。

```js
for (var i = 0; i < 5; ++i) {
  setTimeout(function () {
    console.log(i); // 输出 '5' 五次
  }, 100);  
}
```

  使用 `let` 替换 `var`

```js
// print 1, 2, 3, 4, 5
for (let i = 0; i < 5; ++i) {
  setTimeout(function () {
    console.log(i); // 输出 0, 1, 2, 3, 4
  }, 100);  
}
```


### 我们应该用 `let` 替代 `var` 嗎？

> 不是的，`let` 是新的块作用域。语法强调在 `var` 已经是区块作用域时時，`let` 应该替换 `var` ，否则请不要替换 `var`。`let` 改善了在 JS 作用域的选项，而不是取代。`var` 对于变量依旧是有用的，可被用在整個 function 之中。

### `let` 兼容性

- 在 server 端，比如 Node.js，你现在可以安心的使用 `let`。

- 在 client 端，通过 transpiler（比如 [Traceur](https://github.com/google/traceur-compiler)），可以安心的使用 `let` 语法。否则请在[这里](http://caniuse.com/#search=let)确认你的浏览器是否支持。

### Playground
<div>
  <a class="jsbin-embed" href="http://jsbin.com/yumaye/embed?js,console">JS Bin on jsbin.com</a><script src="http://static.jsbin.com/js/embed.min.js?3.39.11"></script>
</div>

### 更多信息

- [Let keyword vs var keyword](http://stackoverflow.com/questions/762011/let-keyword-vs-var-keyword)
- [For and against let](https://davidwalsh.name/for-and-against-let)
- [Explanation of `let` and block scoping with for loops](http://stackoverflow.com/questions/30899612/explanation-of-let-and-block-scoping-with-for-loops/30900289#30900289).
