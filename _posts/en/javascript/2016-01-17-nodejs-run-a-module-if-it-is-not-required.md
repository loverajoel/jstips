---
layout: post

title: Node.js - Run a module if it is not `required`
tip-number: 17
tip-username: odsdq
tip-username-profile: https://twitter.com/odsdq
tip-tldr: In node, you can tell your program to do two different things depending on whether the code is run from `require('./something.js')` or `node something.js`. This is useful if you want to interact with one of your modules independently.

redirect_from:
  - /en/nodejs-run-a-module-if-it-is-not-required/

categories:
    - en
    - javascript
---

In node, you can tell your program to do two different things depending on whether the code is run from `require('./something.js')` or `node something.js`.  This is useful if you want to interact with one of your modules independently.

```js
if (!module.parent) {
    // ran with `node something.js`
    app.listen(8088, function() {
        console.log('app listening on port 8088');
    })
} else {
    // used with `require('/.something.js')`
    module.exports = app;
}
```

See [the documentation for modules](https://nodejs.org/api/modules.html#modules_module_parent) for more info.