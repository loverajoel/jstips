---
layout: post

title: Easiest way to extract unix timestamp in JS
tip-number: 49
tip-username: nmrony
tip-username-profile: https://github.com/nmrony
tip-tldr: In Javascript you can easily get the unix timestamp

redirect_from:
  - /en/extract-unix-timestamp-easily/

categories:
    - en
    - javascript
---

We frequently need to calculate with unix timestamp. There are several ways to grab the timestamp. For current unix timestamp easiest and fastest way is

```js
const dateTime = Date.now();
const timestamp = Math.floor(dateTime / 1000);
```
or

```js
const dateTime = new Date().getTime();
const timestamp = Math.floor(dateTime / 1000);
```

To get unix timestamp of a specific date pass `YYYY-MM-DD` or `YYYY-MM-DDT00:00:00Z` as parameter of `Date` constructor. For example

```js
const dateTime = new Date('2012-06-08').getTime();
const timestamp = Math.floor(dateTime / 1000);
```
You can just add a `+` sign also when declaring a `Date` object like below

```js
const dateTime = +new Date();
const timestamp = Math.floor(dateTime / 1000);
```
or for specific date

```js
const dateTime = +new Date('2012-06-08');
const timestamp = Math.floor(dateTime / 1000);
```
Under the hood the runtime calls `valueOf` method of the `Date` object. Then the unary `+` operator calls `toNumber()` with that returned value. For detailed explanation please check the following links

* [Date.prototype.valueOf](http://es5.github.io/#x15.9.5.8)
* [Unary + operator](http://es5.github.io/#x11.4.6)
* [toNumber()](http://es5.github.io/#x9.3)
* [Date Javascript MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
* [Date.parse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/parse)
