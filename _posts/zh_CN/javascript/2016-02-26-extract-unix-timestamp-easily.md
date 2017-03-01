---
layout: post

title: 简单获取unix时间戳
tip-number: 49
tip-username: nmrony
tip-username-profile: https://github.com/nmrony
tip-tldr: 在Javascript里，你可以简单的取得unix时间戳

redirect_from:
  - /zh_cn/extract-unix-timestamp-easily/

categories:
    - zh_CN
    - javascript
---


我们经常需要使用unix时间戳计算。有很多方法可以取得unix时间戳。目前取得unix时间戳最简单最快的方法是：

```js
const dateTime = Date.now();
const timestamp = Math.floor(dateTime / 1000);
```
或

```js
const dateTime = new Date().getTime();
const timestamp = Math.floor(dateTime / 1000);
```

要取得一个具体时间的unix时间戳，将`yyyy-mm-dd`或`YYYY-MM-DDT00:00:00Z`作为参数传递给`Date`构造函数。例如

```js
const dateTime = new Date('2012-06-08').getTime();
const timestamp = Math.floor(dateTime / 1000);
```

你还可以像下面一样，在声明`Date`对象的时候添加一个`+`号

```js
const dateTime = +new Date();
const timestamp = Math.floor(dateTime / 1000);
```
或者对于具体时间

```js
const dateTime = +new Date('2012-06-08');
const timestamp = Math.floor(dateTime / 1000);
```

在底层，运行时调用了`Date`对象的`valueOf`方法。然后一元操作符`+`调用了之前返回值的`toNumber()`方法。想要了解更多内容请参考下面链接

* [Date.prototype.valueOf](http://es5.github.io/#x15.9.5.8)
* [Unary + operator](http://es5.github.io/#x11.4.6)
* [toNumber()](http://es5.github.io/#x9.3)
* [Date Javascript MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
* [Date.parse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/parse)
