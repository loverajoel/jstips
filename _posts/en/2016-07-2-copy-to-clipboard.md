---
layout: post

title: Copy to Clipboard
tip-number: 55
tip-username: loverajoel
tip-username-profile: https://twitter.com/loverajoel
tip-tldr: This week I had to create a common "Copy to Clipboard" button, I've never created one before and I want to share with I made it.

categories:
    - en
---

This is a simple tip, this week I had to create a common "Copy to Clipboard" button, I've never created one before and I want to share with I made it.
It's easy, the bad thing is that we must have to add an `<input/>` with the text to be copied to the DOM. Then, we selected the content and executes the copy command with [execCommand](https://developer.mozilla.org/en-US/docs/Web/API/Document/execCommand).
`execCommand('copy')` will copy the actual selected content.

Also, this command that now is supported by all the latest version of browsers, allows us to execute another system commands like `copy`, `cut`, `paste`, and make changes like fonts color, size, and much more.

```js
document.querySelector('#input').select();
document.execCommand('copy');
```

See this in action [here](https://jsbin.com/huhozu/edit?html,js,output)