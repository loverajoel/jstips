---
layout: post

title: Concatenación de Strings segura
tip-number: 19
tip-username: gogainda
tip-username-profile: https://twitter.com/gogainda
tip-tldr: Suponga que tiene un par de variables con tipos desconocidos y desea concatenar en una cadena. Para asegurarse de que la operación aritmética no se puede aplicar durante la concatenación, utilizar concat

redirect_from:
  - /es_es/safe-string-concatenation/

categories:
    - es_ES
    - javascript
---

Suponga que tiene un par de variables con tipos desconocidos y desea concatenar en una cadena. Para asegurarse de que la operación aritmética no se puede aplicar durante la concatenación, utilizar 'concat':

```javascript
var one = 1;
var two = 2;
var three = '3';

var result = ''.concat(one, two, three); //"123"
```

Esta forma de concatenación hace exactamente lo que se espera. Por el contrario, la concatenación con ventajas podría conducir a resultados inesperados:

```javascript
var one = 1;
var two = 2;
var three = '3';

var result = one + two + three; //"33" instead of "123"
```

Hablando de rendimiento, en comparación con el `join` [type](http://www.sitepoint.com/javascript-fast-string-concatenation/) de concatenación, la velocidad de` concat` es más o menos lo mismo.

Puede leer mas sobre `concat` en MDN [page](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/concat).