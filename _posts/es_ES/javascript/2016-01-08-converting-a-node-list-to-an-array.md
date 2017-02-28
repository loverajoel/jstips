---
layout: post

title: Convitiendo una Node List a un Array.
tip-number: 08
tip-username: Tevko
tip-username-profile: https://twitter.com/tevko
tip-tldr: Aquí está una manera rápida, segura y reutilizable para convertir una lista de nodos en un Array de elementos del DOM.

redirect_from:
  - /es_es/converting-a-node-list-to-an-array/

categories:
    - es_ES
    - javascript
---

El método `querySelectorAll` devuelve un array similar a un objeto, llamado una lista de nodos. Estas estructuras de datos se denominan como "Array-like", porque aparecen como un array, pero no se pueden utilizar con los métodos de matriz como `map` y `forEach`. Aquí está una manera rápida, segura y reutilizable para convertir una lista de nodos en un Array de elementos del DOM:

```javascript
const nodelist = document.querySelectorAll('div');
const nodelistToArray = Array.apply(null, nodelist);

//later on ..

nodelistToArray.forEach(...);
nodelistToArray.map(...);
nodelistToArray.slice(...);

//etc...
```

El método `apply` se utiliza para pasar una serie de argumentos a una función con un determinado valor de `this`.[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) afirma que `apply` tendrá un objeto de tipo vector, que es exactamente lo que `querySelectorAll` retorna. Dado que no es necesario especificar un valor para `this` en el contexto de la función, se pasa en `null` o `0`. El resultado es una matriz real de los elementos DOM que contiene todos los métodos de arreglos disponibles.

O si esta utilizando ES2015 puede usar esto [spread operator `...`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)

```js
const nodelist = [...document.querySelectorAll('div')]; // returns a real array

//later on ..

nodelist.forEach(...);
nodelist.map(...);
nodelist.slice(...);

//etc...
```