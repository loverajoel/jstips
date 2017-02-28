---
layout: post

title: 避免修改或傳送 arguments 到其他函式 - 它會影響優化
tip-number: 31
tip-username: berkana
tip-username-profile: https://github.com/berkana
tip-tldr: 在 JavaScript 的函式，變數名稱 `arguments` 讓你可以存取所有傳送到函式的參數。`arguments` 是一個 *類陣列物件*；`arguments` 可以使用陣列表示來存取，而且它有 *length* 屬性，但不具備陣列的 `filter` 和 `map` 以及 `forEach` 的方法。以下程式碼是轉換 `arguments` 到陣列相當普遍的做法。


redirect_from:
  - /zh_tw/avoid-modifying-or-passing-arguments-into-other-functions-it-kills-optimization/

categories:
    - zh_TW
    - javascript
---

### 背景

在 JavaScript 的函式，變數名稱 [`arguments`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments) 讓你可以存取所有傳送到函式的參數。`arguments` 是一個 *類陣列物件*；`arguments` 可以使用陣列表示來存取，而且它有 *length* 屬性，但不具備陣列的 `filter` 和 `map` 以及 `forEach` 的方法。以下程式碼是轉換 `arguments` 到陣列相當普遍的做法。

```js
var args = Array.prototype.slice.call(arguments);
```
將 `arguments` 傳送到 `Array` 原型的上的 `slice` 方法；`slice` 方法回傳淺拷貝的 `arguments` 當作新的陣列物件。一般常見的簡寫方法：

```js
var args = [].slice.call(arguments);
```
在這個情況下，只是呼叫一個空陣列陣列，而不是從 `Array` 原型上呼叫 `slice` 方法。

### 優化

不幸的是，傳送到任何函式呼叫的 `arguments`，造成在 Chrome 和 Node 跳過 JavaScript V8 引擎的優化功能，這可能會導致性能降低。參考這篇 [optimization killers](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers) 文章。傳送 `arguments` 到函式稱為 *leaking `arguments`*。

相反的，假設你需要包含參數的陣列，你可以藉助這個方法：

```js
var args = new Array(arguments.length);
for(var i = 0; i < args.length; ++i) {
  args[i] = arguments[i];
}
```

雖然程式碼更冗長，但是在上線環境增進了效能的優化，所以是值得的。
