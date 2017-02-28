---
layout: post

title: Calcular el valor Max/Min de un array
tip-number: 45
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: Formas de utilizar las funciones Math.max() y Math.min() con array de números
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /es_es/detect-document-ready-in-pure-js/

categories:
    - es_ES
    - javascript
---

Las funciones [Math.max()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/max) and [Math.min()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/min) encontrar el valor máximo y mínimo de los argumentos, respectivamente.

```js
Math.max(1, 2, 3, 4); // 4
Math.min(1, 2, 3, 4); // 1
```

Estas funciones no funcionarán como tal con arrays de números. Sin embargo, hay algunas maneras de evitar esto.

[`Function.prototype.apply()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) le permite llamar a una función con un determinado valor de `this` y un _array_ de argumentos.

```js
var numbers = [1, 2, 3, 4];
Math.max.apply(null, numbers) // 4
Math.min.apply(null, numbers) // 1
```

Pasando el array `numbers` como el segundo argumento de `apply()` resulta en la función invocados con todos los valores en le array como parámetros.

Una manera sencilla con ES2015 de conseguir esto [spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator).

```js
var numbers = [1, 2, 3, 4];
Math.max(...numbers) // 4
Math.min(...numbers) // 1
```

Este operador hace que los valores del array a ser ampliado, o "spread", dentro de argumentos de la función.
