---
layout: post

title: 使用 pure JavaScript 檢查文件是否準備
tip-number: 46
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: 可以跨瀏覽器，而且使用 pure JavaScript 來確認文件是否已經載入完成。
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /zh_tw/detect-document-ready-in-pure-js/

categories:
    - zh_TW
    - javascript
---

可以跨瀏覽器，而且使用 pure JavaScript 來確認文件是否已經載入完成的方式是使用 [`readyState`](https://developer.mozilla.org/en-US/docs/Web/API/Document/readyState)。

```js
if (document.readyState === 'complete') {
	// 網頁已經完全載入
}
```

當文件載入後，你可以檢查文件是否載入完成...


```js
let stateCheck = setInterval(() => {
	if (document.readyState === 'complete') {
    clearInterval(stateCheck);
	 // 文件載入
  }
}, 100);
```

或使用 [onreadystatechange](https://developer.mozilla.org/en-US/docs/Web/Events/readystatechange)...


```js
document.onreadystatechange = () => {
  if (document.readyState === 'complete') {
   // 文件載入
  }
};
```

當 DOM 載入後，使用 `document.readyState === 'interactive'` 來檢查是否載入完成。
