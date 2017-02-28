---
layout: post

title: 更簡單的方式將 indexOf 當作 contains 使用
tip-number: 15
tip-username: jhogoforbroke
tip-username-profile: https://twitter.com/jhogoforbroke
tip-tldr: JavaScript 預設沒有 contain 的方法。如果要檢查字串或是陣列內是否有子字串的存在你可以這樣做。

redirect_from:
  - /zh_tw/even-simpler-way-of-using-indexof-as-a-contains-clause/

categories:
    - zh_TW
    - javascript
---

JavaScript 預設沒有 contain 的方法。如果要檢查字串或是陣列內是否有子字串的存在你可以這樣做：

```javascript
var someText = 'javascript rules';
if (someText.indexOf('javascript') !== -1) {
}

// or
if (someText.indexOf('javascript') >= 0) {
}
```

但是，讓我看一下這些 [Expressjs](https://github.com/strongloop/express) 程式碼片段。

[examples/mvc/lib/boot.js](https://github.com/strongloop/express/blob/2f8ac6726fa20ab5b4a05c112c886752868ac8ce/examples/mvc/lib/boot.js#L26)


```javascript
for (var key in obj) {
  // "reserved" exports
  if (~['name', 'prefix', 'engine', 'before'].indexOf(key)) continue;
```

[lib/utils.js](https://github.com/strongloop/express/blob/2f8ac6726fa20ab5b4a05c112c886752868ac8ce/lib/utils.js#L93)


```javascript
exports.normalizeType = function(type){
  return ~type.indexOf('/')
    ? acceptParams(type)
    : { value: mime.lookup(type), params: {} };
};
```

[examples/web-service/index.js](https://github.com/strongloop/express/blob/2f8ac6726fa20ab5b4a05c112c886752868ac8ce/examples/web-service/index.js#L35)


```javascript
// key 是無效的
if (!~apiKeys.indexOf(key)) return next(error(401, 'invalid api key'));
```

困難的地方是[位元運算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators) **~**，「位元運算符在二進制執行它們的操作，但是它們回傳的是標準 JavaScript 數值」。

它將 `-1` 轉換成 `0`，而 `0` 在 JavaScript 當作 `false`：

```javascript
var someText = 'text';
!!~someText.indexOf('tex'); // someText 包含 "tex" - true
!~someText.indexOf('tex'); // someText 不包含 "tex" - false
~someText.indexOf('asd'); // someText 不包含 "asd" - false
~someText.indexOf('ext'); // someText 包含 "ext" - true
```

### String.prototype.includes()

ES6 提供了 [includes() 方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes)，你可以使用它來判斷字串是否包含在其他字串：

```javascript
'something'.includes('thing'); // true
```

在 ECMAScript 2016（ES7）中，在陣列甚至有可能可以使用這些方法：

```javascript
!!~[1, 2, 3].indexOf(1); // true
[1, 2, 3].includes(1); // true
```

**不幸的是，這只支援在 Chrome、Firefox、Safari 9 或是更高版本的 Edge；在 IE11 或更低版本則無法使用。**
**它最好在被控制的環境下使用。**
