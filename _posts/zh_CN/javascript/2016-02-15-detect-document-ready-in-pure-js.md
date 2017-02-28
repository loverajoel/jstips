---
layout: post

title: 纯JS监听document是否加载完成
tip-number: 46
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: 跨浏览器且纯JavaScript检测document是否加载完成。
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /zh_cn/detect-document-ready-in-pure-js/

categories:
    - zh_CN
    - javascript
---

跨浏览器且纯JavaScript检测document是否加载完成的方法是使用[`readyState`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/readyState).

```js
if (document.readyState === 'complete') {
  // 页面已完全加载
}
```

这样可以在document完全加载时监测到……


```js
let stateCheck = setInterval(() => {
  if (document.readyState === 'complete') {
	clearInterval(stateCheck);
	// document ready
  }
}, 100);
```

或者使用[onreadystatechange](https://developer.mozilla.org/zh-CN/docs/Web/Events/readystatechange)


```js
document.onreadystatechange = () => {
  if (document.readyState === 'complete') {
	// document ready
  }
};
```

使用`document.readyState === 'interactive'`监听DOM是否加载完成。
