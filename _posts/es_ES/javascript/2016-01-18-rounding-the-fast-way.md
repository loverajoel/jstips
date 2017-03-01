---
layout: post

title: Redondeo, la manera mas rápida
tip-number: 18
tip-username: pklinger
tip-username-profile: https://github.com/pklinger
tip-tldr: El tip de hoy es sobre el rendimiento. Nunca llegó a través del operador doble tilde `~~`? A veces también se llama el doble operador NOT (operador de bits). Se puede utilizar como un sustituto más rápido para `Math.floor()`. ¿Porqué es eso?

redirect_from:
  - /es_es/rounding-the-fast-way/

categories:
    - es_ES
    - javascript
---

El tip de hoy es sobre el rendimiento. [Nunca llegó a través del operador dobletilde] (http://stackoverflow.com/questions/5971645/what-is-the-double-tilde-operator-in-javascript) `~~`? A veces también se llama el doble operador NOT (operador de bits). Se puede utilizar como un sustituto más rápido para `Math.floor()`. ¿Porqué es eso?

One bitwise shift `~` transforms the 32 bit converted input into `-(input+1)`. The double bitwise shift therefore transforms the input into `-(-(input + 1)+1)` making it a great tool to round towards 0. For numeric input, it therefore mimics the `Math.ceil()` for negative and `Math.floor()` for positive input. On failure, `0` is returned, which might come in handy sometimes instead of `Math.floor()`, which returns a value of `NaN` on failure.
Un desplazamiento en modo bit `~` transforma 32 bits de entrada `-(input+1)`. Por tanto, el cambio de doble bit a bit transforma la entrada en `-(-(input + 1)+1)` por lo que es una gran herramienta para redondear hacia 0. Para la entrada numérica, de este modo imita el `Math.ceil()` para el negativo y `Math.floor()` para la entrada positiva. En caso de error, se devuelve `0`, lo que podría ser útil a veces en lugar de `Math.floor()`,que devuelve un valor de `NaN` en caso de fallo.

```javascript
// single ~
console.log(~1337)    // -1338

// numeric input
console.log(~~47.11)  // -> 47
console.log(~~-12.88) // -> -12
console.log(~~1.9999) // -> 1
console.log(~~3)      // -> 3

// on failure
console.log(~~[]) // -> 0
console.log(~~NaN)  // -> 0
console.log(~~null) // -> 0

// greater than 32 bit integer fails
console.log(~~(2147483647 + 1) === (2147483647 + 1)) // -> 0
```

A pesar de que `~~` puede funcionar mejor, por el bien de la legibilidad por favor utilice `Math.floor()`.