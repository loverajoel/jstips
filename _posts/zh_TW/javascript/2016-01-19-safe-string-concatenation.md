---
layout: post

title: 安全的使用字串串接
tip-number: 19
tip-username: gogainda
tip-username-profile: https://twitter.com/gogainda
tip-tldr: 假設你有一些不確定的變數類型，而你想將它們串接成字串。可以確定的是，算術運算不是應用在串接的地方，使用 concat 來串接。

redirect_from:
  - /zh_tw/safe-string-concatenation/

categories:
    - zh_TW
    - javascript
---

假設你有一些不確定的變數類型，而你想將它們串接成字串。可以肯定的是，算術運算符不是在串接過程的運用，請使用 `concat`：

```javascript
var one = 1;
var two = 2;
var three = '3';

var result = ''.concat(one, two, three); // "123"
```

這個方法串接結果是你預期的。相反的，透過加號來串接會造成非預期的結果：

```javascript
var one = 1;
var two = 2;
var three = '3';

var result = one + two + three; // "33" 而不是 "123"
```

關於性能部分，與 `join` [類型](http://www.sitepoint.com/javascript-fast-string-concatenation/)比較，串接速度和 `concat` 是差不多的。

你可以在 MDN [網頁](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/concat)上閱讀到更多關於 `concat` 函式的資訊。
