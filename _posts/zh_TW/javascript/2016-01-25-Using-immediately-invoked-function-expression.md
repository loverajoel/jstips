---
layout: post

title: 使用立即函式表達式
tip-number: 25
tip-username: rishantagarwal
tip-username-profile: https://github.com/rishantagarwal
tip-tldr: 稱作「Iffy」（IIFE - immediately invoked function expression）是一個匿名函式表達式，而且可以立即被調用，在 JavaScript 中有一些相當重要的用途。


redirect_from:
  - /zh_tw/Using-immediately-invoked-function-expression/

categories:
    - zh_TW
    - javascript
---

稱作「Iffy」（IIFE - immediately invoked function expression）是一個匿名函式表達式，而且可以立即被調用，在 JavaScript 中有一些相當重要的用途。

```javascript

(function() {
 // Do something​
 }
)()

```

它是一個匿名函式表達式，而且可以立即被調用，在 JavaScript 某些部分中相當重要。

一對括號包著匿名函式，將匿名函式變成函式表達式或變數表達式。我們現在有一個未命名的函式表達式，它不是一個在全域 scope 內的簡單匿名函式或者是其他任何被定義的函式。

同樣的，我們也可以為立即函式表達式命名：

```javascript
(someNamedFunction = function(msg) {
    console.log(msg || "Nothing for today !!")
})(); // 輸出 --> Nothing for today !!​
​
someNamedFunction("Javascript rocks !!"); // 輸出 --> Javascript rocks !!
someNamedFunction(); // 輸出 --> Nothing for today !!​
```

更多細節，請參考以下網址 -
1. [連結一](https://blog.mariusschulz.com/2016/01/13/disassembling-javascripts-iife-syntax)
2. [連結二](http://javascriptissexy.com/12-simple-yet-powerful-javascript-tips/)

效能：
[jsPerf](http://jsperf.com/iife-with-call)
