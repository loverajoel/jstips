---
layout: post

title: Retorno de valores con el operador 'new'
tip-number: 52
tip-username: Morklympious
tip-username-profile: https://github.com/morklympious
tip-tldr: Comprender lo que se devuelve cuando el uso de new vs. sin usar new.

redirect_from:
  - /es_es/get-file-extension/

categories:
    - es_ES
    - javascript
---

Usted va a correr dentro de algunas instancias en las que va a utilizar `new` para asignar nuevos objetos en JavaScript. Se va a volar tu mente a menos que lea este consejo para entender lo que está sucediendo por detrás.

El operador `new` en JavaScript es un operador que, en circunstancias razonables, devuelve una nueva instancia de un objeto. Digamos que tenemos una función constructora:

````js
function Thing() {
  this.one = 1;
  this.two = 2;
}

var myThing = new Thing();

myThing.one // 1
myThing.two // 2
````

__Nota__: `This` se refiere al nuevo objeto creado por `new`. De lo contrario, si `Thing()` se llama sin `new`, __objeto no creado__, y `this` va a apuntar al objeto global, que es `window`. Esto significa que:

1. Usted repentinamente tiene dos nuevas variables globales con nombre `one` y 'two`.
2. `myThing` ahora es undefined, ya que no devuelve nada en `Thing()`.

Ahora que se obtiene ese ejemplo, aquí es donde las cosas se ponen un poco torcidas. Digamos que quiero añadir algo a la función constructora, un poco de sabor:

````js
function Thing() {
  this.one = 1;
  this.two = 2;

  return 5;
}

var myThing = new Thing();
````

Ahora, que hace myThing equal? Es 5? es un objeto? Es mi sentido lisiado de autoestima? El mundo nunca puede saber!

Excepto el mundo sabe:

````js
myThing.one // 1
myThing.two // 2
````

Curiosamente, nunca realmente vemos los cinco que supuestamente 'retorna' de nuestro constructor. Eso es raro, ¿verdad? ¿Qué hace la función? ¿Dónde está el cinco? Vamos a probar con otra cosa.

Vamos a retornar un tipo no primitivo, algo así como un objeto.

````js
function Thing() {
  this.one = 1;
  this.two = 2;

  return {
    three: 3,
    four: 4
  };
}

var myThing = new Thing();
````

Vamos a ver. Un console.log revela todo:

````js
console.log(myThing);
/*
  Object {three: 3, four: 4}
  What happened to this.one and this.two!?
  They've been stomped, my friend.
*/
````

__Aquí es donde aprendemos:__ Cuando se llama a una función con la palabra clave `new`, puede setear propiedades en el uso de la palabra clave `this` (pero probablemente ya lo sabía). La devolución de un valor simple de una función que llamó a la palabra clave `new` no devolverá el valor que ha especificado, pero en su lugar devolverá la instancia `this` de la función (el que se introdujo en propiedades, como `this.one = 1;`).

Sin embargo, el retorno de un no-primitivo, como un `object`,` array`, o `function` será pisar fuerte en la instancia `this`, y volver ese no primitivo en su lugar, arruinando todo el duro trabajo que hizo todo lo posible para asignar `this`.
