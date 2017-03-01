---
layout: post

title: Pseudo parámetros obligatorios en funciones ES6
tip-number: 12
tip-username: Avraam Mavridis
tip-username-profile: https://github.com/AvraamMavridis
tip-tldr: En muchos lenguajes de programación, los parámetros de una función por defecto son obligatorios y el desarrollador tiene que definir explícitamente que un parámetro es opcional.

redirect_from:
  - /es_es/pseudomandatory-parameters-in-es6-functions/

categories:
    - es_ES
    - javascript
---

En muchos lenguajes de programación, los parámetros de una función por defecto son obligatorios y el desarrollador tiene que definir explícitamente que un parámetro es opcional. En Javascript, cada parámetro es opcional, pero puede hacer cumplir este comportamiento sin jugar con el propio cuerpo de una función, aprovechando [** valores predeterminados para los parámetros de es6's **] (http://exploringjs.com/es6/ch_parameter -handling.html # sec_parameter-valores por defecto).

```javascript
const _err = function( message ){
  throw new Error( message );
}

const getSum = (a = _err('a is not defined'), b = _err('b is not defined')) => a + b

getSum( 10 ) // throws Error, b is not defined
getSum( undefined, 10 ) // throws Error, a is not defined
```

 `_err` es una función que lanza inmediatamente un error. Si no se pasa ningún valor para uno de los parámetros, el valor predeterminado se va a utilizar, `_err` serán tratados y se emite un error. Se puede ver más ejemplos para **caracteristicas de parámetros por defecto** en [Mozilla's Developer Network ](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/default_parameters)