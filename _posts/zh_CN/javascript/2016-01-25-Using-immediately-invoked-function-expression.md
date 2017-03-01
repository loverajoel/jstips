---
layout: post

title: 使用立即执行函数表达式
tip-number: 25
tip-username: rishantagarwal 
tip-username-profile: https://github.com/rishantagarwal
tip-tldr: 立即执行函数表达式( IIFE - immediately invoked function expression)是一个立即执行的匿名函数表达式，它在Javascript中有一些很重要的用途。


redirect_from:
  - /zh_cn/Using-immediately-invoked-function-expression/

categories:
    - zh_CN
    - javascript
---

立即执行函数表达式( IIFE - immediately invoked function expression)是一个立即执行的匿名函数表达式，它在Javascript中有一些很重要的用途。

```javascript

(function() {
 // Do something​
 }
)()

```

这是一个立即执行的匿名函数表达式，它在有JavaScript一些特别重要的用途。

两对括号包裹着一个匿名函数，使匿名函数变成了一个函数表达式。于是，我们现在拥有了一个未命名的函数表达式，而不是一个全局作用域下或在任何地方定义的的简单函数。

类似地，我们也可以创建一个命名过的立即执行函数表达式：

```javascript
(someNamedFunction = function(msg) {
	console.log(msg || "Nothing for today !!")
	}) (); // 输出 --> Nothing for today !!​
​
someNamedFunction("Javascript rocks !!"); // 输出 --> Javascript rocks !!
someNamedFunction(); // 输出 --> Nothing for today !!​
```

更多内容, 请参考下面链接 - 
1. [链接 1](https://blog.mariusschulz.com/2016/01/13/disassembling-javascripts-iife-syntax) 
2. [链接 2](http://javascriptissexy.com/12-simple-yet-powerful-javascript-tips/) 

效率:
[jsPerf](http://jsperf.com/iife-with-call)