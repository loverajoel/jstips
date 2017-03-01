---
layout: post

title: 将Node List转换为数组(Array)
tip-number: 08
tip-username: Tevko
tip-username-profile: https://twitter.com/tevko
tip-tldr: 这是一个快速、安全、可重用的方法将node list转换为DOM元素的数组。

redirect_from:
  - /zh_cn/converting-a-node-list-to-an-array/

categories:
    - zh_CN
    - javascript
---

`querySelectorAll`方法返回一个类数组对象称为node list。这些数据结构被称为“类数组”，因为他们看似数组却没有类似`map`、`foreach`这样的数组方法。这是一个快速、安全、可重用的方法将node list转换为DOM元素的数组：

```javascript
const nodelist = document.querySelectorAll('div');
const nodelistToArray = Array.apply(null, nodelist);


//之后 ..

nodelistToArray.forEach(...);
nodelistToArray.map(...);
nodelistToArray.slice(...);


//等...
```

`apply`方法可以在指定`this`时以数组形式向方法传递参数。[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)规定`apply`可以接受类数组对象,恰巧就是`querySelectorAll`方法所返回的内容。如果我们不需要指定方法内`this`的值时传`null`或`0`即可。返回的结果即包含所有数组方法的DOM元素数组。

另外你可以使用`Array.prototype.slice`结合`Function.prototype.call`或`Function.prototype.apply`， 将类数组对象当做`this`传入：

```javascript
const nodelist = document.querySelectorAll('div');
const nodelistToArray = Array.prototype.slice.call(nodelist); // or equivalently Array.prototype.slice.apply(nodelist);

//之后 ..

nodelistToArray.forEach(...);
nodelistToArray.map(...);
nodelistToArray.slice(...);

//等...
```


如果你正在用ES2015你可以使用[展开运算符 `...`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_operator)

```js
const nodelist = [...document.querySelectorAll('div')]; // 返回一个真正的数组

//之后 ..

nodelist.forEach(...);
nodelist.map(...);
nodelist.slice(...);


//等...
```
