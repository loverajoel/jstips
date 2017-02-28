---
layout: post

title: Copy to Clipboard
tip-number: 56
tip-username: loverajoel
tip-username-profile: https://twitter.com/loverajoel
tip-tldr: This week I had to create a common "Copy to Clipboard" button, I've never created one before and I want to share how I made it.
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /en/copy-to-clipboard/

categories:
    - en
    - javascript
---

This is a simple tip, this week I had to create a common "Copy to Clipboard" button, I've never created one before and I want to share how I made it.
It's easy, the bad thing is that we must add an `<input/>` with the text to be copied to the DOM. Then, we selected the content and execute the copy command with [execCommand](https://developer.mozilla.org/en-US/docs/Web/API/Document/execCommand).
`execCommand('copy')` will copy the actual selected content.

Also, this command that now is [supported](http://caniuse.com/#search=execCommand) by all the latest version of browsers, allows us to execute another system commands like `copy`, `cut`, `paste`, and make changes like fonts color, size, and much more.

```js
document.querySelector('#input').select();
document.execCommand('copy');
```

##### Playground
<div>
  <a class="jsbin-embed" href="http://jsbin.com/huhozu/embed?js,output">JS Bin on jsbin.com</a><script src="http://static.jsbin.com/js/embed.min.js?3.39.11"></script>
</div>
