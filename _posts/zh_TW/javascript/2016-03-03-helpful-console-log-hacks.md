---
layout: post

title: 實用的 Console Logging 技巧
tip-number: 50
tip-username: zackhall
tip-username-profile: https://twitter.com/zthall
tip-tldr: 使用條件中斷點的 logging 實用技巧。

redirect_from:
  - /zh_tw/helpful-console-log-hacks/

categories:
    - zh_TW
    - javascript
---

## 使用條件中斷點來記錄資料

當函式被呼叫時，如果你想要在 console 顯示每次記錄  的值，你可以透過條件中斷點來記錄。打開你的開發工具，找到你要 console 出來資料的函式，並設定以下的條件中斷點：

```js
console.log(data.value) && false
```

如果條件中斷點為 true 才會停止頁面。所以，使用條件像是 console.log('foo') && false 可以保證為 false，因為在 AND 條件下有一個 false。所以這不會停止你的頁面，但是還是會 console 你記錄的資料。這也可以使用在記錄你的函式或 callback 被呼叫了多少次。

這裡有一些各個瀏覽器如何設定條件中斷點：[Edge](https://dev.windows.com/en-us/microsoft-edge/platform/documentation/f12-devtools-guide/debugger/#setting-and-managing-breakpoints "Managing Breakpoints in Edge")、[Chrome](https://developer.chrome.com/devtools/docs/javascript-debugging#breakpoints "Managing Breakpoints in Chrome") 和 [Firefox](https://developer.mozilla.org/en-US/docs/Tools/Debugger/How_to/Set_a_conditional_breakpoint "Managing Breakpoints in Firefox") 和 [Safari](https://developer.apple.com/library/mac/documentation/AppleApplications/Conceptual/Safari_Developer_Guide/Debugger/Debugger.html "Managing Breakpoints in Safari")。

## 在 console 顯示函式的變數

你曾經想要 console 顯示函式的變數，但是卻無法看到函式的程式碼嗎？最快速看到函式的程式碼的方式是將函式的變數串接一個空字串強制把它轉成字串來顯示。

```js
console.log(funcVariable + '');
```