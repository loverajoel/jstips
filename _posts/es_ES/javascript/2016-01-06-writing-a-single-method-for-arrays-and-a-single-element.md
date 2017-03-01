---
layout: post

title: Escribir un método único para los arrays y elemento unico
tip-number: 06
tip-username: mattfxyz
tip-username-profile: https://twitter.com/mattfxyz
tip-tldr: En lugar de escribir métodos separados para manejar un array y un único parámetro elemento, escriba sus funciones para que puedan manejar ambos. Esto es similar a la forma en que algunas de las funciones de jQuery trabaja(`css` modificará todos los que coinciden con el selector).

redirect_from:
  - /es_es/writing-a-single-method-for-arrays-and-a-single-element/

categories:
    - es_ES
    - javascript
---

En lugar de escribir métodos separados para manejar un array y un único parámetro elemento, escriba sus funciones para que puedan manejar ambos. Esto es similar a la forma en que algunas de las funciones de jQuery trabaja(`css` modificará todos los que coinciden con el selector).

Sólo tienes que concatenar todo en un array. `Array.concat` aceptará un array o un elemento único.

```javascript
function printUpperCase(words) {
  var elements = [].concat(words);
  for (var i = 0; i < elements.length; i++) {
    console.log(elements[i].toUpperCase());
  }
}
```

`printUpperCase` ya está listo para aceptar un único nodo o un conjunto de nodos como su parámetro.

```javascript
printUpperCase("cactus");
// => CACTUS
printUpperCase(["cactus", "bear", "potato"]);
// => CACTUS
//  BEAR
//  POTATO
```
