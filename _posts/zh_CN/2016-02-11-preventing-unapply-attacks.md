---
layout: post

title: 预防unapply攻击
tip-number: 42
tip-username: emars 
tip-username-profile: https://twitter.com/marseltov
tip-tldr: 冻结内置对象的原型方法。

categories:
    - zh_CN
---

重写内置对象的原型方法，攻击者可以重写代码达到暴漏和修改已绑定参数的函数。这在es5的方法实现`polyfill`时是一个严重的安全漏洞。

```js
// bind polyfill 示例
function bind(fn) {
  var prev = Array.prototype.slice.call(arguments, 1);
  return function bound() {
    var curr = Array.prototype.slice.call(arguments, 0);
    var args = Array.prototype.concat.apply(prev, curr);
    return fn.apply(null, args);
  };
}


// unapply攻击
function unapplyAttack() {
  var concat = Array.prototype.concat;
  Array.prototype.concat = function replaceAll() {
    Array.prototype.concat = concat; // restore the correct version
    var curr = Array.prototype.slice.call(arguments, 0);
    var result = concat.apply([], curr);
    return result;
  };
}
```

上面的函数声明忽略了函数bind的`prev`参数，意味着调用`unapplyAttack`之后首次调用`.concat`将会抛出错误。

使用[Object.freeze](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)，可以使对象不可变，你可以防止任何内置对象原型方法被重写。


```js
(function freezePrototypes() {
  if (typeof Object.freeze !== 'function') {
    throw new Error('Missing Object.freeze');
  }
  Object.freeze(Object.prototype);
  Object.freeze(Array.prototype);
  Object.freeze(Function.prototype);
}());
```

你可以[在这里](https://glebbahmutov.com/blog/unapply-attack/)阅读更多关于unapply攻击。