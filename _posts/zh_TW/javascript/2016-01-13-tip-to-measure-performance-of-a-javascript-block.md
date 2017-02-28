---
layout: post

title: 測量 JavaScript 程式碼區塊性能的 tip
tip-number: 13
tip-username: manmadareddy
tip-username-profile: https://twitter.com/manmadareddy
tip-tldr: 如果要快速的測量 JavaScript 程式碼區塊性能的話，我們可以使用 console 函式像是 `console.time(label)` 和 `console.timeEnd(label)`。

redirect_from:
  - /zh_tw/tip-to-measure-performance-of-a-javascript-block/

categories:
    - zh_TW
    - javascript
---

如果要快速的測量 JavaScript 程式碼區塊性能的話，我們可以使用 console 函式像是
[`console.time(label)`](https://developer.chrome.com/devtools/docs/console-api#consoletimelabel) 和 [`console.timeEnd(label)`](https://developer.chrome.com/devtools/docs/console-api#consoletimeendlabel)。

```javascript
console.time("Array initialize");
var arr = new Array(100),
    len = arr.length,
    i;

for (i = 0; i < len; i++) {
    arr[i] = new Object();
};
console.timeEnd("Array initialize"); // 輸出：陣列初始化：0.711ms
```

更多資訊：
[Console object](https://github.com/DeveloperToolsWG/console-object)、
[Javascript benchmarking](https://mathiasbynens.be/notes/javascript-benchmarking)。

範例：[jsfiddle](https://jsfiddle.net/meottb62/) - [codepen](http://codepen.io/anon/pen/JGJPoa)（在瀏覽器 console 下輸出）。

> 注意：根據 [Mozilla](https://developer.mozilla.org/en-US/docs/Web/API/Console/time) 建議，不該使用在上線環境下使用此方法，只能使用在開發環境。
