---
layout: post

title: Map() to the rescue; adding order to Object properties
tip-number: 32
tip-username: loverajoel
tip-username-profile: https://twitter.com/loverajoel
tip-tldr: An Object it is an unordered collection of properties... that means that if you are trying to save ordered data inside an Object, you have to review it because properties order in objects are not guaranteed.
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /en/map-to-the-rescue-adding-order-to-object-properties/

categories:
    - en
    - javascript
---

## Object properties order

> An object is a member of the type Object. It is an unordered collection of properties each of which contains a primitive value, object, or function. A function stored in a property of an object is called a method. [ECMAScript](http://www.ecma-international.org/publications/files/ECMA-ST-ARCH/ECMA-262,%203rd%20edition,%20December%201999.pdf)

Take a look in action

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
Each browser have his own rules about the order in objects bebause technically, order is unspecified.

## How to solve this?

### Map

Using a new ES6 feature called Map. A [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) object iterates its elements in insertion order — a `for...of` loop returns an array of [key, value] for each iteration. 

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

### Hack for old browsers

Mozilla suggest:
> So, if you want to simulate an ordered associative array in a cross-browser environment, you are forced to either use two separate arrays (one for the keys and the other for the values), or build an array of single-property objects, etc.

```js
// Using two separate arrays
var objectKeys = [z, @, b, 1, 5];
for (item in objectKeys) {
	myObject[item]
...

// Build an array of single-property objects
var myData = [{z: 1}, {'@': 2}, {b: 3}, {1: 4}, {5: 5}];
```
