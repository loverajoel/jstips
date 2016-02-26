---
layout: post

title: Easiest way to extract unix timestamp in JS
tip-number: 49
tip-username: nmrony
tip-username-profile: https://github.com/nmrony
tip-tldr: In Javascript you can easily get the unix timestamp

categories:
    - en
---

We frequently need to calculate with unix timestamp. There are several ways to grab the timestamp. For current unix timestamp easiest and fastest way is
```js
const timestamp = Date.now();
```
or

```js
const timestamp = new Date().getTime();
```

To get unix timestamp of a specific date pass `yyyy-mm-dd` as a parameter of `Date` constructor. For example
```js
const timestamp = new Date('2012-06-08').getTime()
```
You can just add a `+` sign also when declaring a `Date` object like below

```js
const timestamp = +new Date()
```
or for specific date

```js
const timestamp = +new Date('2012-06-08')
```
Under the hood the runtime calls `valueOf` method of the `Date` object. Then the unary `+` operator calls `toNumber()` with that returned value. For detailed explanation please check the following links

* [Date.prototype.valueOf](http://es5.github.io/#x15.9.5.8)
* [Unary + operator](http://es5.github.io/#x11.4.6)
* [toNumber()](http://es5.github.io/#x9.3)