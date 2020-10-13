---
layout: post

title: Flattening multidimensional Arrays in JavaScript
tip-number: 38
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: Three different solutions to merge multidimensional array into a single array.
tip-writer-support: https://www.coinbase.com/loverajoel


redirect_from:
  - /en/flattening-multidimensional-arrays-in-javascript/

categories:
    - en
    - javascript
---

These are the three known ways to merge multidimensional array into a single array.

Given this array:

```js
var myArray = [[1, 2],[3, 4, 5], [6, 7, 8, 9]];
```

We wanna have this result:

```js
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Solution 1: Using [`concat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) and [`apply()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

```js
var myNewArray = [].concat.apply([], myArray);
// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Solution 2: Using [`reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce#Flatten_an_array_of_arrays)

```js
var myNewArray = myArray.reduce(function(prev, curr) {
  return prev.concat(curr);
});
// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Solution 3:

```js
var myNewArray3 = [];
for (var i = 0; i < myArray.length; ++i) {
  for (var j = 0; j < myArray[i].length; ++j)
    myNewArray3.push(myArray[i][j]);
}
console.log(myNewArray3);
// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Solution 4: Using [spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator) in ES6

```js
var myNewArray4 = [].concat(...myArray);
console.log(myNewArray4);
// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Solution 5: Using [`flat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/flat) in ES10

```js
var myNewArray5 = myArray.flat();
console.log(myNewArray5);
// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

Take a look [here](https://jsbin.com/janana/edit?js,console) these 4 algorithms in action.

For infinitely nested array try Lodash [flattenDeep()](https://lodash.com/docs#flattenDeep).

If you are curious about performance, [here](http://jsperf.com/flatten-an-array-loop-vs-reduce/6) a test for check how it works.
