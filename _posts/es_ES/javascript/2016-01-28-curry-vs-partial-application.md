---
layout: post

title: Currying vs partial application
tip-number: 28
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: Currying and partial application son dos maneras de transformar una funcion en otra funcion generalidad muy pequeña.


redirect_from:
  - es_es/curry-vs-partial-application/

categories:
    - es_ES
    - javascript
---

**Currying**

Currying toma una función


f: X * Y -> R

y lo convierte en una función

f': X -> (Y -> R)

En lugar de llamar f con dos argumentos, invocamos f' con el primer argumento. El resultado es una función que entonces llamamos con el segundo argumento para producir el resultado.
Por lo tanto, si el f no es comparable se invoca como

f(3,5)

entonces el f' comparables es invocada como

f(3)(5)

Por ejemplo:
Uncurried add()

```javascript

function add(x, y) {
  return x + y;
}

add(3, 5);   // returns 8
```

Curried add()

```javascript
function addC(x) {
  return function (y) {
    return x + y;
  }
}

addC(3)(5);   // returns 8
```

**El algoritmo para currying.** 

Curry toma una función binaria y devuelve una función unaria, función que devuelve una función unaria.

curry: (X × Y → R) → (X → (Y → R))

Codigo Javascript:

```javascript
function curry(f) {
  return function(x) {
    return function(y) {
      return f(x, y);
    }
  }
}
```

**Partial application**

Partial application toma una funcion

f: X * Y -> R

y un valor fijo para el primer argumento para producir una nueva función

f`: Y -> R

f' hace lo mismo que f, pero sólo tiene que completar el segundo parámetro.

Por ejemplo: almacenando el primer argumento de la función de añadir a 5 resulta la función más 5.

```javascript
function plus5(y) {
  return 5 + y;
}

plus5(3);  // returns 8
```

**El algoritmo de partial application.**

partApply toma una función y un valor binario y produce una función unaria.

partApply : ((X × Y → R) × X) → (Y → R)

Codigo Javascript:

```javascript
function partApply(f, x) {
  return function(y) {
    return f(x, y);
  }
}
```
