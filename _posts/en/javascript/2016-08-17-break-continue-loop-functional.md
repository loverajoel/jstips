---
layout: post

title: Breaking or continuing loop in functional programming
tip-number: 58
tip-username: vamshisuram
tip-username-profile: https://github.com/vamshisuram
tip-tldr: A common task for us is iterate over a list looking for a value or values, but we can't return from inside a loop so we will have to iterate the whole array, even if the item we search is the first in the list, in this tip we will see how to short circuit with `.some` and `.every`.


redirect_from:
  - /en/break-continue-loop-functional/

categories:
    - en
    - javascript
---


A common requirement of iteration is cancelation. Using `for` loops we can `break` to end iteration early.

```javascript
const a = [0, 1, 2, 3, 4];
for (var i = 0; i < a.length; i++) {
  if (a[i] === 2) {
    break; // stop the loop
  }
  console.log(a[i]);
}
//> 0, 1
```

Another common requirement is to close over our variables.

A quick approach is to use `.forEach` but
then we lack the ability to `break`. In this situation the closest we get is `continue` functionality through `return`.

```javascript
[0, 1, 2, 3, 4].forEach(function(val, i) {
  if (val === 2) {
    // how do we stop?
    return true;
  }
  console.log(val); // your code
});
//> 0, 1, 3, 4
```

The `.some` is a method on Array prototype. It tests whether some element in the array passes the test implemented by the provided function. If any value is returning true, then it stops executing. Here is a [MDN link](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/some) for more details.

An example quoted from that link

```javascript
const isBiggerThan10 = numb => numb > 10;

[2, 5, 8, 1, 4].some(isBiggerThan10);  // false
[12, 5, 8, 1, 4].some(isBiggerThan10); // true
```

Using `.some` we get iteration functionally similar to `.forEach` but with the ability to `break` through `return` instead.

```javascript
[0, 1, 2, 3, 4].some(function(val, i) {
  if (val === 2) {
    return true;
  }
  console.log(val); // your code
});
//> 0, 1
```


You keep returning `false` to make it `continue` to next item. When you return `true`, the loop will `break` and `a.some(..)` will `return` `true`.

```javascript
// Array contains 2
const isTwoPresent = [0, 1, 2, 3, 4].some(function(val, i) {
  if (val === 2) {
    return true; // break
  }
});
console.log(isTwoPresent);
//> true
```

Also there is `.every`, which can be used. We have to return the opposite boolean compared to `.some`.

##### Playground
<div>
  <a class="jsbin-embed" href="http://jsbin.com/jopeji/embed?js,console">JS Bin on jsbin.com</a><script src="http://static.jsbin.com/js/embed.min.js?3.39.11"></script>
</div>
