---
layout: post

title: Insertar elemento en un array
tip-number: 00
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: Insertar un elemento en un array es una tarea diaria básica. Puedes añadir elementos al final del array usando push, al principio usando unshift, o entremdias usando splice.


categories:
    - es
---

Insertar un elemento en un array es una tarea diaria básica. Puedes añadir elementos al final del array usando push, al principio usando unshift, o entremdias usando splice.

Estos son métodos conocidos, pero no significa que no haya una forma más eficiente. Aquí vamos:

Añadir un elemento al final del array es fácil con push(), pero hay una forma más eficiente.

```javascript
var arr = [1,2,3,4,5];

arr.push(6);
arr[arr.length] = 6; // 43% más rápido en Chrome 47.0.2526.106 en un Mac OS X 10.11.1
```
Ambos métodos modifican el array original. ¿No me crees? Comprueba el [jsperf](http://jsperf.com/push-item-inside-an-array)

Ahora, si lo que intentas es añadir un elemento al principio del array:

```javascript
var arr = [1,2,3,4,5];

arr.unshift(0);
[0].concat(arr); // 98% más rápido Chrome 47.0.2526.106 en un Mac OS X 10.11.1
```
Un poco más de detalle: unshift edita el array original; concat retorna un nuevo array. [jsperf](http://jsperf.com/unshift-item-inside-an-array)

Añadir elementos entremedias del array es fácil con splice, y es la forma más eficiente de hacerlo.

```javascript
var elementos = ['uno', 'dos', 'tres', 'cuatro'];
elementos.splice(elementos.length / 2, 0, 'hola');
```

He intentado ejecutar estos tests en varios navegadores y sistemas operativos y el resultado ha sido similar. Espero que estos consejos sean útiles y te inste a realizar tus propios tests!
