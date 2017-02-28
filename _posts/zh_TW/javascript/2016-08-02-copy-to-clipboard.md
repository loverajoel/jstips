---
layout: post

title: 複製到剪貼版
tip-number: 56
tip-username: loverajoel
tip-username-profile: https://twitter.com/loverajoel
tip-tldr: 本週我建立了一個常見的「複製到剪貼版」按鈕，我以前不曾做過這樣的功能，我想分享我如何實作它。
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /zh_tw/copy-to-clipboard/

categories:
    - zh_TW
    - javascript
---

這是一個簡單的 tip，本週我建立了一個常見的「複製到剪貼版」按鈕，我以前不曾做過這樣的功能，我想分享我如何實作它。
它很簡單，比較麻煩的是我們必須加入一個 `<input/>` 與文字複製到 DOM。我們選擇內容並執行 [execCommand](https://developer.mozilla.org/en-US/docs/Web/API/Document/execCommand) 複製指令。
`execCommand('copy')` 將複製時間被選擇的內容

這個指令目前[支援](http://caniuse.com/#search=execCommand)所有最新的瀏覽器，允許我們執行其他系統指令，像是：`copy`、`cut`、`paste` 和改變字體顏色、大小等等。

```js
document.querySelector('#input').select();
document.execCommand('copy');
```

具體呈現請看參考[這裡](https://jsbin.com/huhozu/edit?html,js,output)
