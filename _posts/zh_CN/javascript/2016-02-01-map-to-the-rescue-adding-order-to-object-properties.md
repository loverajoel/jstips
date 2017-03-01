---
layout: post

title: Map()的营救；使对象属性有顺序
tip-number: 32
tip-username: loverajoel
tip-username-profile: https://twitter.com/loverajoel
tip-tldr: 对象是一个无序的对象集合。这意味着如果你想在对象里保存有序的数据，你需要重新处理它，因为对象里的数据不保证是有序的。
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /zh_cn/map-to-the-rescue-adding-order-to-object-properties/

categories:
    - zh_CN
    - javascript
---

## 对象属性顺序

> 一个对象是一个`Object`类型的实例。它是由一些未排序的元素组成的集合，其中包含了原始变量，对象，和函数。一个对象的属性所对应的函数被称为方法。[ECMAScript](http://www.ecma-international.org/publications/files/ECMA-ST-ARCH/ECMA-262,%203rd%20edition,%20December%201999.pdf)

实际看一下

```js
var myObject = {
	z: 1,
	'@': 2,
	b: 3,
	1: 4,
	5: 5
};
console.log(myObject) // Object {1: 4, 5: 5, z: 1, @: 2, b: 3}

for (item in myObject) {...
// 1
// 5
// z
// @
// b
```

因为技术实现，每个浏览器在排序时都有自己的规则，顺序是不确定的。

## 怎么解决呢?

### Map

使用ES6的新特性Map。[Map](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Map) 对象以插入的顺序遍历元素。`for...of`循环为每一次循环返回一个[key, value]数组。

```js
var myObject = new Map();
myObject.set('z', 1);
myObject.set('@', 2);
myObject.set('b', 3);
for (var [key, value] of myObject) {
  console.log(key, value);
...
// z 1
// @ 2
// b 3
```

### 攻克老浏览器

Mozilla 建议:
> 所以，如果过你想在跨浏览器环境中模拟一个有序的关联数组，你要么使用两个分开的数组（一个保存key，另一个保存value）,要么构建一个单属性对象(single-property objects)的数组。

```js
// 使用分开的数组
var objectKeys = [z, @, b, 1, 5];
for (item in objectKeys) {
	myObject[item]
...

// 构建一个单属性对象(single-property objects)的数组
var myData = [{z: 1}, {'@': 2}, {b: 3}, {1: 4}, {5: 5}];
```