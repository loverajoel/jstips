---
layout: post

title: Manera aún más sencilla de contener la cláusula al usar `indexOf`
tip-number: 15
tip-username: jhogoforbroke
tip-username-profile: https://twitter.com/jhogoforbroke
tip-tldr: JavaScript por defecto no tiene un método contains. Y para comprobar la existencia de una subcadena en una cadena o un elemento de un array puede hacer esto.

redirect_from:
  - /es_es/even-simpler-way-of-using-indexof-as-a-contains-clause/

categories:
    - es_ES
    - javascript	
---

JavaScript por defecto no tiene un método contains. Y para comprobar la existencia de una subcadena en una cadena o un elemento de un array puede hacer esto:

```javascript
var someText = 'javascript rules';
if (someText.indexOf('javascript') !== -1) {
}

// or
if (someText.indexOf('javascript') >= 0) {
}
```

Pero vea esto [Expressjs](https://github.com/strongloop/express) code snippets.

[examples/mvc/lib/boot.js](https://github.com/strongloop/express/blob/2f8ac6726fa20ab5b4a05c112c886752868ac8ce/examples/mvc/lib/boot.js#L26)


```javascript
for (var key in obj) {
  // "reserved" exports
  if (~['name', 'prefix', 'engine', 'before'].indexOf(key)) continue;
```

[lib/utils.js](https://github.com/strongloop/express/blob/2f8ac6726fa20ab5b4a05c112c886752868ac8ce/lib/utils.js#L93)


```javascript
exports.normalizeType = function(type){
  return ~type.indexOf('/')
    ? acceptParams(type)
    : { value: mime.lookup(type), params: {} };
};
```

[examples/web-service/index.js](https://github.com/strongloop/express/blob/2f8ac6726fa20ab5b4a05c112c886752868ac8ce/examples/web-service/index.js#L35)


```javascript
// key is invalid
if (!~apiKeys.indexOf(key)) return next(error(401, 'invalid api key'));
```

El gotcha es el [bitwise operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators) **~**, "Operadores bit a bit realizan sus operaciones en representaciones binarias, sino que devuelven valores numéricos estándar de JavaScript."

Transforma `-1` en `0`, and `0` evalúa como false JavaScript:

```javascript
var someText = 'text';
!!~someText.indexOf('tex'); // someText contains "tex" - true
!~someText.indexOf('tex'); // someText NOT contains "tex" - false
~someText.indexOf('asd'); // someText doesn't contain "asd" - false
~someText.indexOf('ext'); // someText contains "ext" - true
```

### String.prototype.includes()

ES6 introdujo [includes() method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes) y se puede usar para determinar si o no una cadena incluye otra cadena:

```javascript
'something'.includes('thing'); // true
```

Con ECMAScript 2016 (ES7) incluso es posible utilizar estas técnicas con Arrays:

```javascript
!!~[1, 2, 3].indexOf(1); // true
[1, 2, 3].includes(1); // true
```

**Sólo se admite en Chrome, Firefox, Safari 9 o superior y Edge; No EI11 o inferior.**
**Es mejor utilizados en ambientes controlados.**