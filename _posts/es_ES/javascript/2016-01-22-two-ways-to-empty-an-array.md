---
layout: post

title: Dos formas de vacia un array
tip-number: 22
tip-username: microlv
tip-username-profile: https://github.com/microlv
tip-tldr: En JavaScript cuando se quiere vaciar un array, hay una muchas maneras, pero esta es la mas potente.

redirect_from:
  - /es_es/two-ways-to-empty-an-array/

categories:
    - es_ES
    - javascript
---

Se define un array y desea vaciar su contenido.
Por lo general, usted lo haría así:

```javascript
// define Array
var list = [1, 2, 3, 4];
function empty() {
    //empty your array
    list = [];
}
empty();
```
Pero hay otra manera de vaciar un array que es más performante.

Debe utilizar un código como este:

```javascript
var list = [1, 2, 3, 4];
function empty() {
    //empty your array
    list.length = 0;
}
empty();
```

* `list = []` asigna una referencia a un nuevo array a una variable, mientras que las otras referencias no se ven afectadas.
Lo que significa que las referencias a los contenidos del array anterior todavía se mantienen en la memoria, lo que lleva a pérdidas de memoria.

* `list.length = 0` borra todo el contenido del array, lo que afecta otras referencias.

In other words, if you have two references to the same array (`a = [1,2,3]; a2 = a;`), and you delete the array's contents using `list.length = 0`, both references (a and a2) will now point to the same empty array. (So don't use this technique if you don't want a2 to hold an empty array!)
En otras palabras, si usted tiene dos referencias a el mismo array (`a = [1,2,3]; a2 = a;`), y se elimina el contenido del array usando `list.length = 0`, ambas referencias (a and a2) se apuntan ahora al mismo array vacío. (Así que no se utilice esta técnica si usted no quiere a2 para sostener un array vacío!)

Piense en lo que tendra esta salida:

```js
var foo = [1,2,3];
var bar = [1,2,3];
var foo2 = foo;
var bar2 = bar;
foo = [];
bar.length = 0;
console.log(foo, bar, foo2, bar2);

// [] [] [1, 2, 3] []
```

Stackoverflow mas detalles:
[difference-between-array-length-0-and-array](http://stackoverflow.com/questions/4804235/difference-between-array-length-0-and-array)
