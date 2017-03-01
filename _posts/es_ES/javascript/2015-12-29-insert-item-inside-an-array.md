---
layout: post

title: Insertar elemento dentro de un Array
tip-number: 00
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: La inserción de un elemento en un array existente, es una tarea común diaria. Se pueden añadir elementos al final de un array mediante push, al principio usando unshift, al medio que usa splice.
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /es_es/insert-item-inside-an-array/

categories:
    - es_ES
    - javascript
---

La inserción de un elemento en un array existente, es una tarea común diaria. Se pueden añadir elementos al final de un array mediante push, al principio usando unshift, al medio que usa splice.

Esos son los métodos conocidos, pero no quiere decir que no hay una manera más performante. Aquí vamos:

Agragar un elemento al final de un array es fácil con push(), pero hay una manera más performante.

```javascript
var arr = [1,2,3,4,5];

arr.push(6);
arr[arr.length] = 6; // 43% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
Ambos métodos modifican el array original. No lo cree? [jsperf](http://jsperf.com/push-item-inside-an-array)

Ahora bien, si estamos tratando de añadir un elemento al principio de un array:

```javascript
var arr = [1,2,3,4,5];

arr.unshift(0);
[0].concat(arr); // 98% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
Aquí un poco más de detalle: unshift editó el array original; concat devuelve un nuevo array.[jsperf](http://jsperf.com/unshift-item-inside-an-array)

Para añadir elementos en el medio de un array es fácil con splice, y que es la forma mas potente para hacerlo.

```javascript
var items = ['one', 'two', 'three', 'four'];
items.splice(items.length / 2, 0, 'hello');
```

Traté de correr estas pruebas en distintos navegadores y sistemas operativos y los resultados fueron similares. Espero que estos consejos les sea de utilidad para usted y animar a llevar a cabo sus propias pruebas!