---
layout: post

title: 检查某对象是否有某属性
tip-number: 10
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: 这是一些检查某对象是否有某属性的方法。
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /zh_cn/check-if-a-property-is-in-a-object/

categories:
    - zh_CN
    - javascript
---

当你需要检查某属性是否存在于一个[对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Working_with_Objects)，你可能会这样做：

```javascript
var myObject = {
  name: '@tips_js'
};


if (myObject.name) { ... }

```

这是可以的，但是你需要知道有两种原生方法可以解决此类问题。[`in` 操作符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/in) 和 [`Object.hasOwnProperty`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty)，任何继承自`Object`的对象都可以使用这两种方法。

### 看一下较大的区别

```javascript
var myObject = {
  name: '@tips_js'
};

myObject.hasOwnProperty('name'); // true
'name' in myObject; // true


myObject.hasOwnProperty('valueOf'); // false, valueOf 继承自原型链
'valueOf' in myObject; // true

```


两者检查属性的深度不同，换言之`hasOwnProperty`只在本身有此属性时返回true,而`in`操作符不区分属性来自于本身或继承自原型链。

这是另一个例子

```javascript
var myFunc = function() {
  this.name = '@tips_js';
};
myFunc.prototype.age = '10 days';

var user = new myFunc();

user.hasOwnProperty('name'); // true

user.hasOwnProperty('age'); // false, 因为age来自于原型链
```

[在线示例](https://jsbin.com/tecoqa/edit?js,console)!

同样建议阅读关于检查对象是否包含属性时常见错误的[讨论](https://github.com/loverajoel/jstips/issues/62)。
