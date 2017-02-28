---
layout: post

title: 在 JavaScript 簡單取得 unix timestamp
tip-number: 49
tip-username: nmrony
tip-username-profile: https://github.com/nmrony
tip-tldr: 在 JavaScript 你可以簡單取得 unix timestamp

redirect_from:
  - /zh_tw/extract-unix-timestamp-easily/

categories:
    - zh_TW
    - javascript
---

我們經常需要計算 unix 的 timestamp。有許多方式可以取得 timestamp。目前取得 unix timestamp 最簡單和快速的方式是：

```js
const dateTime = Date.now();
const timestamp = Math.floor(dateTime / 1000);
```

或

```js
const dateTime = new Date().getTime();
const timestamp = Math.floor(dateTime / 1000);
```

如果要取得特定的 unix timestamp 傳送一個 `YYYY-MM-DD` 或 `YYYY-MM-DDT00:00:00Z` 參數到 `Date` 的建構子。例如：

```js
const timestamp = new Date('2012-06-08').getTime()
```

當你宣告一個 `Date` 物件，也可以加上 `+` 符號：

```js
const dateTime = +new Date();
const timestamp = Math.floor(dateTime / 1000);
```
或指定日期

```js
const dateTime = +new Date('2012-06-08');
const timestamp = Math.floor(dateTime / 1000);
```
在執行時呼叫了 `Date` 物件的 `valueOf` 方法。`+` 運算子呼叫了 `toNumber()` 和回傳的值。更多細節的說明請參考以下的連結。

* [Date.prototype.valueOf](http://es5.github.io/#x15.9.5.8)
* [Unary + operator](http://es5.github.io/#x11.4.6)
* [toNumber()](http://es5.github.io/#x9.3)
* [Date Javascript MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
* [Date.parse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/parse)
