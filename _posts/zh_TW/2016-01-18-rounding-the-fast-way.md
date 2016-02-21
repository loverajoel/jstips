---
layout: post

title: 捨入最快的方法
tip-number: 18
tip-username: pklinger
tip-username-profile: https://github.com/pklinger
tip-tldr: 今天的小知識是關於性能的部分。曾經使用過雙波浪 `~~` 運算符嗎？有時候也被稱為 雙 NOT 位元運算符。你可以使用它來替代 `Math.floor()` 更為快速。這是為什麼呢？

categories:
    - zh_TW
---

今天的小知識是關於性能的部分。[曾經使用過雙波浪](http://stackoverflow.com/questions/5971645/what-is-the-double-tilde-operator-in-javascript) `~~` 運算符嗎？有時候也被稱為 雙 NOT 位元運算符。你可以使用它來替代 `Math.floor()` 更為快速。這是為什麼呢？

單位元移位運算符 `~` 將輸入的 32 位元轉換成 `-(input+1)`。因此，雙位元移位運算成為更好的工具，將輸入轉換成 `-(-(input + 1)+1)` 更趨近 0。對於數字輸入，負數就像使用 `Math.ceil()` 而正數就像使用 `Math.floor()`。若失敗的話，則回傳 `0`，當 `Math.floor()` 失敗回傳 `NaN` 時，或許此方法可以替代 `Math.floor()`。

```javascript
// 單 ~
console.log(~1337)    // -1338

// 數字輸入
console.log(~~47.11)  // -> 47
console.log(~~-12.88) // -> -12
console.log(~~1.9999) // -> 1
console.log(~~3)      // -> 3

// 失敗
console.log(~~[]) // -> 0
console.log(~~NaN)  // -> 0
console.log(~~null) // -> 0

// 大於 32 位的整數失敗
console.log(~~(2147483647 + 1) === (2147483647 + 1)) // -> 0
```

雖然 `~~` 可以讓性能更好，但是為了增加程式碼可讀性，請使用 `Math.floor()`。
