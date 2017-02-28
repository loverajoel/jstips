---
layout: post

title: 在 JavaScript 使用嚴格模式
tip-number: 07
tip-username: nainslie
tip-username-profile: https://twitter.com/nat5an
tip-tldr: JavaScript 嚴格模式讓開發者可以寫出更「安全」的 JavaScript 程式碼。

redirect_from:
  - /zh_tw/use-strict-and-get-lazy/

categories:
    - zh_TW
    - javascript
---

JavaScript 嚴格模式讓開發者可以寫出更「安全」的 JavaScript 程式碼。

預設情況下，JavaScript 允許開發者的粗心行為，例如，當我們引用一個沒有要求我們由「var」宣告的變數。或許這個對於一個剛入門的開發者相當方便，當變數名稱拼寫錯誤或者是不小心參考到其他的 scope，這些都是許多錯誤的來源。

開發者喜歡讓電腦幫我們做一些無聊的工作，然後自動幫我們確認工作上的錯誤。這就是 JavaScript 的 「嚴格模式」（use strict）幫我們做的，將錯誤轉換成 JavaScript 錯誤。

我們把這個指令放在 js 檔案的頂端：

```javascript
// 整個 script 使用嚴格模式
"use strict";
var v = "Hi!  I'm a strict mode script!";
```

或是在函式內：

```javascript
function f()
{
  // 函式內使用嚴格模式
  'use strict';
  function nested() { return "And so am I!"; }
  return "Hi!  I'm a strict mode function!  " + nested();
}
function f2() { return "I'm not strict."; }
```

透過 JavaScript 檔案或函式內引入這個指令，我們直接讓 JavaScript 引擎執行嚴格模式來禁止一些在大型 JavaScript 專案不良的行為。除了其他之外，嚴格模式改變了以下的行為：

* 只有被宣告的「var」變數才可以被引用。
* 嘗試寫入唯讀的變數會造成錯誤。
* 你只能透過「new」keyword 才可以呼叫建構子。
* 「this」不再隱式的綁定到全域的物件。
* 對 eval() 有嚴格的限制。
* 防止你使用保留字元或特殊字元當作變數名稱。

嚴格模式對於你的新專案是很棒的，但是對於引入一些大部分沒有使用舊的專案是一個挑戰。如果你將 js 檔案編譯在一起到你的大項目的話，可能會造成所有的檔案都執行在嚴格模式下，造成一些問題。

它不是一個語法，但它是一個文字上的表達，在早期版本的 JavaScript 被忽略了。
嚴格模式支援以下：

* Internet Explorer from version 10.
* Firefox from version 4.
* Chrome from version 13.
* Safari from version 5.1.
* Opera from version 12.

[嚴格模式的詳細說明，請參考 MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)。
