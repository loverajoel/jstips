---
layout: post

title: 复制到粘贴板
tip-number: 56
tip-username: loverajoel
tip-username-profile: https://twitter.com/loverajoel
tip-tldr: 本周我做了一个简单的“复制到剪贴板”按钮，这是我第一次做这种功能，向大家分享一下我的实现方法。
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /zh_cn/copy-to-clipboard/

categories:
    - zh_CN
    - javascript
---

这是一个简单的小知识，本周我做了一个简单的“复制到剪贴板”按钮，这是我第一次做这种功能，向大家分享一下我的实现方法。

这很简单，比较麻烦的是我们必须为需要复制的文本增加`<input/>`标签。之后我们选择要复制的内容然后调用复制命令[execCommand](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/execCommand).
`execCommand('copy')` 将会复制被选择的内容。

此方法目前被所有最新版本的浏览器[支持](http://caniuse.com/#search=execCommand)，它可以让我们执行如`复制`、`剪切`、`粘贴`等命令，还可以改变字体颜色、大小等。

```js
document.querySelector('#input').select();
document.execCommand('copy');
```

具体表现看[这里](https://jsbin.com/huhozu/edit?html,js,output)
