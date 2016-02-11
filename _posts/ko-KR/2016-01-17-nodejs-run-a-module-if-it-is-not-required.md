---
layout: post

title: Node.js - `required`가 아니면 모듈을 실행하라
tip-number: 17
tip-username: odsdq
tip-username-profile: https://twitter.com/odsdq
tip-tldr: 노드에서 `require('./something.js')`냐 `node something.js`냐에 따라 프로그램한테 두개의 다른 일을 명령할 수 있다. 모듈과 독립적으로 상호 작용하려면 이 방법은 유용하다.

categories:
    - ko
---
<translator: https://github.com/tisohjung>

노드에서 `require('./something.js')`냐 `node something.js`냐에 따라 프로그램한테 두개의 다른 일을 명령할 수 있다. 모듈과 독립적으로 상호 작용하려면 이 방법은 유용하다.

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

[더 많은 정보는 모듈에 대한 도큐먼트를 보자](https://nodejs.org/api/modules.html#modules_module_parent).