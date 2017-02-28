---
layout: post

title: Node.js - 執行尚未被 required 的模組
tip-number: 17
tip-username: odsdq
tip-username-profile: https://twitter.com/odsdq
tip-tldr: 在 nodejs，你可以讓你的程式取決於 `require('./something.js')` 或 `node something.js` 這兩種不同的方式來執行你的程式碼。如果你想要將你的獨立模組交互使用是非常有用的。

redirect_from:
  - /zh_tw/nodejs-run-a-module-if-it-is-not-required/

categories:
    - zh_TW
    - javascript
---

在 nodejs，你可以讓你的程式取決於 `require('./something.js')` 或 `node something.js` 這兩種不同的方式來執行你的程式碼。如果你想要將你的獨立模組交互使用是非常有用的。

```js
if (!module.parent) {
    // 透過 `node something.js` 執行
    app.listen(8088, function() {
        console.log('app listening on port 8088');
    })
} else {
    // 使用 `require('/.something.js')` 方法
    module.exports = app;
}
```

更多資訊請參考 [nodejs modules 官方文件](https://nodejs.org/api/modules.html#modules_module_parent)。
