---
layout: post

title: 將參數傳送到 callback 函式
tip-number: 16
tip-username: minhazav
tip-username-profile: https://twitter.com/minhazav
tip-tldr: 預設情況下，你不能傳送參數給 callback 函式，但是你可以利用 JavaScrip closure scope 的優點將參數傳給 callback 函式。

redirect_from:
  - /zh_tw/passing-arguments-to-callback-functions/

categories:
    - zh_TW
    - javascript
---

預設情況下，你不能傳送參數給 callback 函式。例如：

```js
function callback() {
  console.log('Hi human');
}

document.getElementById('someelem').addEventListener('click', callback);

```

你可以利用 JavaScript 閉包（closure）scope 的優點傳送參數給 callback 函式。看一下這個範例：

```js
function callback(a, b) {
  return function() {
    console.log('sum = ', (a+b));
  }
}

var x = 1, y = 2;
document.getElementById('someelem').addEventListener('click', callback(x, y));

```

### 什麼是閉包（closure）？

Closures 指的是一個獨立的變數函式。換句話說，在閉包中定義的函式「記得」它被建立時的環境。在 [MDN 文件](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)了解更多。

當 callback 函式被呼叫時，這些方法的參數 `x` 和 `y` 都會在 callback 函式的範圍內。

另一個方法你可以使用 `bind`。例如：

```js
var alertText = function(text) {
  alert(text);
};

document.getElementById('someelem').addEventListener('click', alertText.bind(this, 'hello'));
```
兩種方法上有細微的性能上的差別，請參考 [jsperf](http://jsperf.com/bind-vs-closure-23)。
