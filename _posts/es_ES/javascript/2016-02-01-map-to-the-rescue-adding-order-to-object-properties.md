---
layout: post

title: Map() al rescate; añadir orden a las propiedades de los Objetos.
tip-number: 32
tip-username: loverajoel
tip-username-profile: https://twitter.com/loverajoel
tip-tldr: Un objeto es una colección desordenada de propiedades... que significa que si está tratando de guardar los datos ordenados dentro de un objeto, hay que revisarlo debido a que las propiedades de orden en los objetos no están garantizados.
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /es_es/map-to-the-rescue-adding-order-to-object-properties/

categories:
    - es_ES
    - javascript
---

## Propiedades de orden del Objeto

> Un objeto es un miembro del tipo de objeto. Es una colección desordenada de las propiedades de cada uno de los cuales contiene un valor primitivo, objeto o función. Una función almacenada en una propiedad de un objeto se llama un método.[ECMAScript](http://www.ecma-international.org/publications/files/ECMA-ST-ARCH/ECMA-262,%203rd%20edition,%20December%201999.pdf)

Veamos en acción

```js
var myObject = {
	z: 1,
	'@': 2,
	b: 3,
	1: 4,
	5: 5
};
console.log(myObject) // Object {1: 4, 5: 5, z: 1, @: 2, b: 3}

for (item in myObject) {...
// 1
// 5
// z
// @
// b
```
Cada navegador tiene sus propias reglas sobre el orden en los objetos porque técnicamente, el orden no se especifica.

## Como solucionar esto?

### Map

Usando una nueva característica de ES6 llamada Map. [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) objeto itera sus elementos con el fin de inserción - un `for...of` devuelve un array de [clave, valor] para cada iteración.

```js
var myObject = new Map();
myObject.set('z', 1);
myObject.set('@', 2);
myObject.set('b', 3);
for (var [key, value] of myObject) {
  console.log(key, value);
...
// z 1
// @ 2
// b 3
```

### Hack para navegadores antiguos

Sugerencias de Mozilla:
> Por lo tanto, si desea simular el orden asociado al array en un entorno cross-browser, se ve obligado a usar dos array independientes (uno para las key y el otro para los valores), o construir una array de objetos de single-property, etc.

```js
// usando dos arrays separados
var objectKeys = [z, @, b, 1, 5];
for (item in objectKeys) {
	myObject[item]
...

// Creando un array de objetos de single-property
var myData = [{z: 1}, {'@': 2}, {b: 3}, {1: 4}, {5: 5}];
```
