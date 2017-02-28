---
layout: post

title: Deduplicate an Array
tip-number: 37
tip-username: danillouz
tip-username-profile: https://www.twitter.com/danillouz
tip-tldr: How to remove duplicate elements, of different data types, from an Array.


redirect_from:
  - /en/deduplicate-an-array/

categories:
    - en
    - javascript
---

# Primitives
If an Array only contains primitive values, we can deduplicate it by
only using the [`filter`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) and [`indexOf`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf) methods.

```javascript
var deduped = [ 1, 1, 'a', 'a' ].filter(function (el, i, arr) {
	return arr.indexOf(el) === i;
});

console.log(deduped); // [ 1, 'a' ]
```

## ES2015
We can write this in a more compact way using an [arrow function](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions).

```javascript
var deduped = [ 1, 1, 'a', 'a' ].filter( (el, i, arr) => arr.indexOf(el) === i);

console.log(deduped); // [ 1, 'a' ]
```

But with the introduction of [Sets](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set) and the [`from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) method, we can achieve the same
result in a more concise way.

```javascript
var deduped = Array.from( new Set([ 1, 1, 'a', 'a' ]) );

console.log(deduped); // [ 1, 'a' ]
```

# Objects
We can't use the same approach when the elements are Objects,
because Objects are stored by reference and primitives are stored
by value.

```javascript
1 === 1 // true

'a' === 'a' // true

{ a: 1 } === { a: 1 } // false
```

Therefore we need to change our approach and use a hash table.

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

```javascript
var hashTable = {};

hashTable[1] = true;
hashTable['1'] = true;

console.log(hashTable); // { '1': true }
```

However, because we're using [`JSON.stringify`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify), keys that are of the
type `String`, will be stored as an escaped string value, giving us unique
keys in our `hashTable`.

```javascript
var hashTable = {};

hashTable[JSON.stringify(1)] = true;
hashTable[JSON.stringify('1')] = true;

console.log(hashTable); // { '1': true, '\'1\'': true }
```

This means duplicate elements of the same value, but of a different type,
will still be deduplicated using the same implementation.

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

# Resources
## Methods
* [`filter`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
* [`indexOf`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)
* [`from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
* [`JSON.stringify`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)

## ES2015
* [arrow functions](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
* [Sets](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)

## Stack overflow
* [remove duplicates from array](http://stackoverflow.com/questions/9229645/remove-duplicates-from-javascript-array/9229821#9229821)
