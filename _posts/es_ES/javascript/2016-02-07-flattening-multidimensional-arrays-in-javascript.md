---
layout: post

title: Arrays multidimensionales en JavaScript
tip-number: 38
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: Tres soluciones diferentes para combinar arrays multidimensional en un sola arrays.
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /es_es/flattening-multidimensional-arrays-in-javascript/

categories:
    - es_ES
    - javascript
---

Estas son las tres formas conocidas para fusionar arrays multidimensional en una sola arrays.

Dado el array:

```js
var myArray = [[1, 2],[3, 4, 5], [6, 7, 8, 9]];
```

Queremos tener este resultado:

```js
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Solucion 1: usando [`concat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) y [`apply()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

```js
var myNewArray = [].concat.apply([], myArray);
// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Solucion 2: usando [`reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce#Flatten_an_array_of_arrays)

```js
var myNewArray = myArray.reduce(function(prev, curr) {
  return prev.concat(curr);
});
// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Solucion 3:

```js
var myNewArray3 = [];
for (var i = 0; i < myArray.length; ++i) {
  for (var j = 0; j < myArray[i].length; ++j)
    myNewArray3.push(myArray[i][j]);
}
console.log(myNewArray3);
// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```
Echar un vistazo [here](https://jsbin.com/qeqicu/edit?js,console) estos 3 algoritmos en accion.

Para array infinitamente anidado probar Underscore [flatten()](https://github.com/jashkenas/underscore/blob/master/underscore.js#L501).

Si tiene curiosidad por la performance, [here](http://jsperf.com/flatten-an-array-loop-vs-reduce/6).