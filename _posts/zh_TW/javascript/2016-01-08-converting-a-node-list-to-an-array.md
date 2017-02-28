---
layout: post

title: 將 Node List 轉換成陣列
tip-number: 08
tip-username: Tevko
tip-username-profile: https://twitter.com/tevko
tip-tldr: 這是快速，安全，可重複使用的方式，將 Node List 轉換成 DOM 元素的陣列。

redirect_from:
  - /zh_tw/converting-a-node-list-to-an-array/

categories:
    - zh_TW
    - javascript
---

`querySelectorAll` 方法回傳一個類似陣列的物件稱為 Node List。這些資料結構簡稱為「類陣列」，因為他們和陣列很相似，但是不能使用陣列的方法像是 `map` 和 `forEach`。這是快速，安全，可重複使用的方式，將 Node List 轉換成 DOM 元素的陣列：

```javascript
const nodelist = document.querySelectorAll('div');
const nodelistToArray = Array.apply(null, nodelist);

// 之後 ..

nodelistToArray.forEach(...);
nodelistToArray.map(...);
nodelistToArray.slice(...);

// 等等...
```

`apply` 方法將參數陣列傳送給一個函式與給定 this 的值。根據 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) ，`apply` 採用類陣列物件，而這剛好就是 `querySelectorAll` 方法所回傳的內容。如果我們不需要在函式的上下文（context）中指定 `this` ，我們可以傳送 `null` 或 `0`。這個結果實際上是一個 DOM 元素陣列，包含所有可用的陣列方法。

或者，假設你使用 ES2015 你可以使用[展開運算符 `...`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)。

```js
const nodelist = [...document.querySelectorAll('div')]; // 回傳一個實際的陣列

// 之後 ..

nodelist.forEach(...);
nodelist.map(...);
nodelist.slice(...);

// 等等...
```
