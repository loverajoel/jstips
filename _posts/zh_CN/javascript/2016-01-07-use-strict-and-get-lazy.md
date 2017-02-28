---
layout: post

title: 使用"use strict" 变得懒惰
tip-number: 07
tip-username: nainslie
tip-username-profile: https://twitter.com/nat5an
tip-tldr: JavaScript的严格模式使开发者更容易写出“安全”的代码。

redirect_from:
  - /zh_cn/use-strict-and-get-lazy/

categories:
    - zh_CN
    - javascript
---

（译者注：此片翻译较渣，欢迎指正，建议大家[阅读原文](http://www.jstips.co/en/use-strict-and-get-lazy/)或直接阅读[MDN对严格模式的中文介绍](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode) 并欢迎PR）

JavaScript的严格模式使开发者更容易写出“安全”的代码。

通常情况下，JavaScript允许程序员相当粗心，比如你可以引用一个从未用"var"声明的变量。或许对于一个刚入门的开发者来说这看起来很方便，但这也是变量拼写错误或者从作用域外引用变量时引发的一系列错误的原因。

程序员喜欢电脑帮我们做一些无聊的工作，喜欢它自动的检查我们工作上的错误。这就是"use strict"帮我们做的，它把我们的错误转变为了JavaScript错误。

我们把这个指令放在js文件顶端来使用它:

```javascript
// 全脚本严格模式
"use strict";
var v = "Hi!  I'm a strict mode script!";
```


或者放在一个方法内：

```javascript
function f()
{

  // 方法级严格模式
  'use strict';
  function nested() { return "And so am I!"; }
  return "Hi!  I'm a strict mode function!  " + nested();
}
function f2() { return "I'm not strict."; }
```


通过在JavaScript文件或方法内引入此指令，使JavaScript引擎运行在严格模式下，这直接禁止了许多大项目中不受欢迎的操作。另外，严格模式也改变了以下行为：
* 只有被"var"声明过的变量才可以引用
* 试图写只读变量时将会报错
* 只能通过"new"关键字调用构造方法
* "this"不再隐式的指向全局变量
* 对eval()有更严格的限制
* 防止你使用预保留关键字命名变量

严格模式对于新项目来说是很棒的，但对于一些并没有使用它的老项目来说，引入它也是很有挑战性的。如果你把所有js文件都连接到一个大文件中的话，可能导致所有文件都运行在严格模式下，这可能也会有一些问题。

它不是一个声明，而是一个表达式，被低版本的JavaScript忽略。
严格模式的支持情况：
* Internet Explorer 10+
* Firefox 4+
* Chrome 13+
* Safari 5.1+
* Opera 12+


[MDN对严格模式的全面介绍](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode)
