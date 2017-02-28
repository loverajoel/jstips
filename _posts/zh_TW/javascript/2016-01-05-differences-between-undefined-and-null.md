---
layout: post

title: undefined 和 null 的差別
tip-number: 05
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: 了解 `undefined` 和 `null` 的差別。
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /zh_tw/differences-between-undefined-and-null/

categories:
    - zh_TW
    - javascript
---

- `undefined` 意思是變數沒有被宣告，或者是已經宣告了，但是沒有賦值。
- `null` 意思是「沒有值」的值。
- Javascript 將未賦值的變數的預設值設為 `undefined`。
- Javascript 從來不會將值設定為 `null`。這是讓開發者用來宣告 `var` 是沒有值的。
- `undefined` 不是一個有效的 JSON，而 `null` 是有效的。
- `undefined` 的類型（typeof） 是 `undefined`。
- `null` 的類型（typeof）是一個 `object`。[為什麼？](http://www.2ality.com/2013/10/typeof-null.html)
- 它們都是原始（primitives）型別。
- 它們都是 [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)
  (`Boolean(undefined) // false`, `Boolean(null) // false`)。
- 你可以判斷一個變數是否為 [undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)。

  ```javascript
  typeof variable === "undefined"
```
- 你可以判斷一個變數是否為 [null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null)。

  ```javascript
  variable === null
```
- **雙等號**運算符認為它們是相等的，但是**三等號**比較時是不相等的。

  ```javascript
  null == undefined // true

  null === undefined // false
```
