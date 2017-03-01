---
layout: post

title: Node.js - 运行未被引用的模块
tip-number: 17
tip-username: odsdq
tip-username-profile: https://twitter.com/odsdq
tip-tldr: 在Node里,你可以让你的程序根据其运行自`require('./something.js')`或者`node something.js`而做不同的处理。如果你想与你的一个独立的模块进行交互，这是非常有用的。

redirect_from:
  - /zh_cn/nodejs-run-a-module-if-it-is-not-required/

categories:
    - zh_CN
    - javascript
---

在Node里,你可以让你的程序根据其运行自`require('./something.js')`或者`node something.js`而做不同的处理。如果你想与你的一个独立的模块进行交互，这是非常有用的。

```js
if (!module.parent) {
    // 通过 `node something.js` 启动
    app.listen(8088, function() {
        console.log('app listening on port 8088');
    })
} else {
    // 通过 `require('/.something.js')` 被引用
    module.exports = app;
}
```

更多内容请看 [modules的文档](https://nodejs.org/api/modules.html#modules_module_parent)
