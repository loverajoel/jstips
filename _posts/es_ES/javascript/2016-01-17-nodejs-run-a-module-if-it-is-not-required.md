---
layout: post

title: Node.js - ejecutar un módulo si no es `required`
tip-number: 17
tip-username: odsdq
tip-username-profile: https://twitter.com/odsdq
tip-tldr: En Node, puede decir que su programa va a hacer dos cosas diferentes dependiendo de si se ejecuta el código `require('./something.js')` o `node something.js`. Esto es útil si desea interactuar con uno de sus módulos de forma independiente.

redirect_from:
  - /es_es/nodejs-run-a-module-if-it-is-not-required/

categories:
    - es_ES
    - javascript
---

En Node, puede decir que su programa va a hacer dos cosas diferentes dependiendo de si se ejecuta el código `require('./something.js')` o `node something.js`. Esto es útil si desea interactuar con uno de sus módulos de forma independiente.

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

Ver [the documentation for modules](https://nodejs.org/api/modules.html#modules_module_parent) para mas informacion.