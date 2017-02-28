---
layout: post

title: Converting a Node List to an Array
tip-number: 08
tip-username: Tevko
tip-username-profile: https://twitter.com/tevko
tip-tldr: Here's a quick, safe, and reusable way to convert a node list into an array of DOM elements.

redirect_from:
  - /en/converting-a-node-list-to-an-array/

categories:
    - en
    - javascript
---

The `querySelectorAll` method returns an array-like object called a node list. These data structures are referred to as "Array-like", because they appear as an array, but can not be used with array methods like `map` and `forEach`. Here's a quick, safe, and reusable way to convert a node list into an array of DOM elements:

```javascript
const nodelist = document.querySelectorAll('div');
const nodelistToArray = Array.apply(null, nodelist);

//later on ..

nodelistToArray.forEach(...);
nodelistToArray.map(...);
nodelistToArray.slice(...);

//etc...
```

The `apply` method is used to pass an array of arguments to a function with a given `this` value. [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) states that `apply` will take an array-like object, which is exactly what `querySelectorAll` returns. Since we don't need to specify a value for `this` in the context of the function, we pass in `null` or `0`. The result is an actual array of DOM elements which contains all of the available array methods.

Alternatively you can use `Array.prototype.slice` combined with `Function.prototype.call` or `Function.prototype.apply` passing the array-like object as the value of `this`:

```javascript
const nodelist = document.querySelectorAll('div');
const nodelistToArray = Array.prototype.slice.call(nodelist); // or equivalently Array.prototype.slice.apply(nodelist);

//later on ..

nodelistToArray.forEach(...);
nodelistToArray.map(...);
nodelistToArray.slice(...);

//etc...
```

Or if you are using ES2015 you can use the [spread operator `...`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)

```js
const nodelist = [...document.querySelectorAll('div')]; // returns a real array

//later on ..

nodelist.forEach(...);
nodelist.map(...);
nodelist.slice(...);

//etc...
```
