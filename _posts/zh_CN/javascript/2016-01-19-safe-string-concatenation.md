---
layout: post

title: 安全的字符串拼接
tip-number: 19
tip-username: gogainda
tip-username-profile: https://twitter.com/gogainda
tip-tldr: 假如你需要拼接一些不确定类型的变量为字符串，你需要确保算术运算符在你拼接时不会起作用。使用concat

redirect_from:
  - /zh_cn/safe-string-concatenation/

categories:
    - zh_CN
    - javascript
---

假如你需要拼接一些不确定类型的变量为字符串，你需要确保算术运算符在你拼接时不会起作用。使用concat：

```javascript
var one = 1;
var two = 2;
var three = '3';

var result = ''.concat(one, two, three); //"123"
```

这应该就是你所期望的拼接结果。如果不这样，拼接时加号可能会导致你意想不到的结果：

```javascript
var one = 1;
var two = 2;
var three = '3';

var result = one + two + three; //"33" instead of "123"
```

关于性能,与用[```join```](http://www.sitepoint.com/javascript-fast-string-concatenation/)来拼接字符串相比 ```concat```的效率是几乎一样的。

你可以在[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)了解更多关于```concat```方法的内容。
