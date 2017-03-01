---
layout: post

title: 向回调方法传递参数
tip-number: 16
tip-username: minhazav
tip-username-profile: https://twitter.com/minhazav
tip-tldr: 通常下，你并不能给回调函数传递参数，但是你可以借助Javascript闭包的优势来传递参数给回调函数。

redirect_from:
  - /zh_cn/passing-arguments-to-callback-functions/

categories:
    - zh_CN
    - javascript
---

通常下，你并不能给回调函数传递参数。 比如:

```js
function callback() {
  console.log('Hi human');
}

document.getElementById('someelem').addEventListener('click', callback);
```

你可以借助Javascript闭包的优势来传递参数给回调函数。看这个例子:

```js
function callback(a, b) {
  return function() {
    console.log('sum = ', (a+b));
  }
}

var x = 1, y = 2;
document.getElementById('someelem').addEventListener('click', callback(x, y));
```

**什么是闭包?**
闭包是指函数有自由独立的变量。换句话说，定义在闭包中的函数可以“记忆”它创建时候的环境。想了解更多请[参考MDN的文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures)。

这种方法使参数`x`和`y`在回调方法被调用时处于其作用域内。

另一个办法是使用`bind`方法。比如:

```js
var alertText = function(text) {
  alert(text);
};

document.getElementById('someelem').addEventListener('click', alertText.bind(this, 'hello'));
```

两种方法之间有着微小的性能差异,请看[jsperf](http://jsperf.com/bind-vs-closure-23).
