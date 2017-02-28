---
layout: post

title: Deduplique un Array
tip-number: 37
tip-username: danillouz
tip-username-profile: https://www.twitter.com/danillouz
tip-tldr: Cómo eliminar elementos duplicados, de diferentes tipos de datos, a partir de un Array.

redirect_from:
  - /es_es/deduplicate-an-array/

categories:
    - es_ES
    - javascript
---

# Primitivos
Si una matriz sólo contiene valores primitivos, podemos desduplicar
solo utilizando [`filter`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) and [`indexOf`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf) methods.

```javascript
var deduped = [ 1, 1, 'a', 'a' ].filter(function (el, i, arr) {
	return arr.indexOf(el) === i;
});

console.log(deduped); // [ 1, 'a' ]
```

## ES2015
Podemos escribir esto de una manera más compacta utilizando [arrow function](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions).

```javascript
var deduped = [ 1, 1, 'a', 'a' ].filter( (el, i, arr) => arr.indexOf(el) === i);

console.log(deduped); // [ 1, 'a' ]
```

Sin embargo, con la introducción de [Sets](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set) y de [`from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) se puede lograr lo mismo como resultado de una manera más concisa.

```javascript
var deduped = Array.from( new Set([ 1, 1, 'a', 'a' ]) );

console.log(deduped); // [ 1, 'a' ]
```

# Objects
No podemos usar el mismo enfoque cuando los elementos son Objects,
Dado que los Objects se almacenan como referencia y se almacenan primitivas
por valor.

```javascript
1 === 1 // true

'a' === 'a' // true

{ a: 1 } === { a: 1 } // false
```

Por lo tanto tenemos que cambiar nuestro enfoque y utilizar una tabla hash.

```javascript
function dedup(arr) {
	var hashTable = {};

	return arr.filter(function (el) {
		var key = JSON.stringify(el);
		var match = Boolean(hashTable[key]);

		return (match ? false : hashTable[key] = true);
	});
}

var deduped = dedup([
	{ a: 1 },
	{ a: 1 },
	[ 1, 2 ],
	[ 1, 2 ]
]);

console.log(deduped); // [ {a: 1}, [1, 2] ]
```

Because a hash table in javascript is simply an `Object`, the keys
will always be of the type `String`. This means that normally we can't
distinguish between strings and numbers of the same value, i.e. `1` and
`'1'`.
Debido a una tabla hash en javascript es simplemente un `Object`, las claves
siempre será del tipo `string`. Esto significa que normalmente no podemos
distinguir entre cadenas y números del mismo valor, es decir `1` y
`'1'`.

```javascript
var hashTable = {};

hashTable[1] = true;
hashTable['1'] = true;

console.log(hashTable); // { '1': true }
```

Sin embargo, debido a que estamos utilizando [`JSON.stringify`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify), key que son del tipo `String`, se almacena como un valor de cadena escapada, que nos da única key en nuestra `hashTable`.

```javascript
var hashTable = {};

hashTable[JSON.stringify(1)] = true;
hashTable[JSON.stringify('1')] = true;

console.log(hashTable); // { '1': true, '\'1\'': true }
```

Esto significa elementos duplicados del mismo valor, pero de un tipo diferente,
aún serán deduplicables utilizando la misma aplicación.

```javascript
var deduped = dedup([
	{ a: 1 },
	{ a: 1 },
	[ 1, 2 ],
	[ 1, 2 ],
	1,
	1,
	'1',
	'1'
]);

console.log(deduped); // [ {a: 1}, [1, 2], 1, '1' ]
```

# Recursos
## Metodos
* [`filter`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
* [`indexOf`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)
* [`from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
* [`JSON.stringify`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)

## ES2015
* [arrow functions](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
* [Sets](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)

## Stack overflow
* [remove duplicates from array](http://stackoverflow.com/questions/9229645/remove-duplicates-from-javascript-array/9229821#9229821)
