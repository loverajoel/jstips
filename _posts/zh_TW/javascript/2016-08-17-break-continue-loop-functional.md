---
layout: post

title: 在 functional programming break 或 continue 迴圈
tip-number: 58
tip-username: vamshisuram
tip-username-profile: https://github.com/vamshisuram
tip-tldr: 迭代一個陣列來尋找值是很平常的事，如果我要搜尋的值是在陣列第一個，也不能直接從迴圈內部回傳，我們需要迭代整個陣列。在這個 tip 我們將看到如何使用 `.some` 和 `.every` 快速完成迭代。


redirect_from:
  - /zh_tw/break-continue-loop-functional/

categories:
    - zh_TW
    - javascript
---


取消迭代是常見的需求。使用 `for` 迴圈我們可以 `break` 讓迭代提早結束。

```javascript
const a = [0, 1, 2, 3, 4];
for (var i = 0; i < a.length; i++) {
  if (a[i] === 2) {
    break; // stop the loop
  }
  console.log(a[i]);
}
//> 0, 1
```

另一個常見的需求是結束我們的變數。

一個快速的方式是使用 `.forEach`，但是我們沒有辦法使用 `break`。在這個情況我們要讓 forEach 透過 `return` 來更貼近 `continue` 的功能。

```javascript
[0, 1, 2, 3, 4].forEach(function(val, i) {
  if (val === 2) {
    // 我們要如何停止？
    return true;
  }
  console.log(val); // 你的程式碼
});
//> 0, 1, 3, 4
```

`.some` 是 Array 的原型（prototype）。它透過提供的 function 測試陣列內的元素是否滿足，如果任何值回傳 true，它將停止執行。這裡是 [MDN 連結](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/some) 有更多關於 `some` 的細節。

引用以上連結內的範例：

```javascript
const isBiggerThan10 = numb => numb > 10;

[2, 5, 8, 1, 4].some(isBiggerThan10);  // false
[12, 5, 8, 1, 4].some(isBiggerThan10); // true
```

使用 `.some` 我們取得像是 `.forEach` 迭代的功能和透過 `return` 來替代 `break` 的方式。

```javascript
[0, 1, 2, 3, 4].some(function(val, i) {
  if (val === 2) {
    return true;
  }
  console.log(val); // 你的程式碼
});
//> 0, 1
```


保持回傳 `false` 來確保`持續`迭代到下一個元素。當你回傳 `true` 時，迴圈將 `break` 且 `a.some(..)` 將 `return` `true`。

```javascript
// Array contains 2
const isTwoPresent = [0, 1, 2, 3, 4].some(function(val, i) {
  if (val === 2) {
    return true; // break
  }
});
console.log(isTwoPresent);
//> true
```

還有 `.every` 也可以使用。我們要回傳和 `.some` 相反的 boolean 值。

##### Playground
<div>
  <a class="jsbin-embed" href="http://jsbin.com/jopeji/embed?js,console">JS Bin on jsbin.com</a><script src="http://static.jsbin.com/js/embed.min.js?3.39.11"></script>
</div>
