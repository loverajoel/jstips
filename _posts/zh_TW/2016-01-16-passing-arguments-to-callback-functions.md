---
layout: post

title: 將參數傳送到 callback 函式
tip-number: 16
tip-username: minhazav
tip-username-profile: https://twitter.com/minhazav
tip-tldr: JavaScript 模組以及建構步驟變得更多更複雜，但對於新的框架樣板呢？

categories:
    - zh_TW
---

預設情況下，你不能傳送參數給 callback 函式。例如：

```js
function callback() {
  console.log('Hi human');
}

document.getElementById('someelem').addEventListener('click', callback);

```

你在 JavaScript 利用閉包範圍的優點傳送參數給 callback 函式。看一下這個範例：

```js
function callback(a, b) {
  return function() {
    console.log('sum = ', (a+b));
  }
}

var x = 1, y = 2;
document.getElementById('someelem').addEventListener('click', callback(x, y));

```

### 什麼是閉包？

閉包是指引用獨立（自由）變數的函式。換句話說，在閉包中定義的函式「記得」它被建立時的環境。在 [MDN 文件](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)了解更多。

當 callback 函式被呼叫時，這些方法的參數 `x` 和 `y` 都會在 callback 函式的範圍內。

另一個方法你可以使用 `bind`。例如：

```js
var alertText = function(text) {
  alert(text);
};

document.getElementById('someelem').addEventListener('click', alertText.bind(this, 'hello'));
```
兩種方法上有細微的性能上的差別，請參考 [jsperf](http://jsperf.com/bind-vs-closure-23)。
