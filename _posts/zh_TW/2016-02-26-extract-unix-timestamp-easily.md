---
layout: post

title: 在 JavaScript 簡單取得 unix timestamp
tip-number: 49
tip-username: nmrony
tip-username-profile: https://github.com/nmrony
tip-tldr: 在 JavaScript 你可以簡單取得 unix timestamp

categories:
    - zh_TW
---

我們經常需要計算 unix 的 timestamp。有許多方式可以取得 timestamp。目前取得 unix timestamp 最簡單和快速的方式是：

```js
const timestamp = Date.now();
```
or

```js
const timestamp = new Date().getTime();
```

如果要取得特定的 unix timestamp 傳送一個 `yyyy-mm--dd` 參數到 `Date` 的建構子。例如：

```js
const timestamp = new Date('2012-06-08').getTime()
```

當你宣告一個 `Date` 物件，也可以加上 `+` 符號：

```js
const timestamp = +new Date()
```
或指定日期

```js
const timestamp = +new Date('2012-06-08')
```
在執行時呼叫了 `Date` 物件的 `valueOf` 方法。`+` 運算子呼叫了 `toNumber()` 和回傳的值。更多細節的說明請參考以下的連結。

* [Date.prototype.valueOf](http://es5.github.io/#x15.9.5.8)
* [Unary + operator](http://es5.github.io/#x11.4.6)
* [toNumber()](http://es5.github.io/#x9.3)
