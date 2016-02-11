---
layout: post

title: Preventing Unapply Attacks
tip-number: 42
tip-username: emars 
tip-username-profile: https://twitter.com/marseltov
tip-tldr: Freeze the builtin prototypes.

categories:
    - en
---

By overriding the builtin prototypes, attackers can rewrite code to expose and change bound arguments. This can be a serious security hole that works by exploting a polyfill es5 methods.

```js
// example bind polyfill
function bind(fn) {
  var prev = Array.prototype.slice.call(arguments, 1);
  return function bound() {
    var curr = Array.prototype.slice.call(arguments, 0);
    var args = Array.prototype.concat.apply(prev, curr);
    return fn.apply(null, args);
  };
}


// unapply-attack
function unapplyAttack() {
  var concat = Array.prototype.concat;
  Array.prototype.concat = function replaceAll() {
    Array.prototype.concat = concat; // restore the correct version
    var curr = Array.prototype.slice.call(arguments, 0);
    var result = concat.apply([], curr);
    return result;
  };
}
```

The above function discards the `prev` array from the bind meaning that any `.concat` the first concat call following using the unapply attack will throw an error.

By using [Object.freeze](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze), making an object immutable, you prevent any overriding of the builtin object prototypes. 


```js
(function freezePrototypes() {
  if (typeof Object.freeze !== 'function') {
    throw new Error('Missing Object.freeze');
  }
  Object.freeze(Object.prototype);
  Object.freeze(Array.prototype);
  Object.freeze(Function.prototype);
}());
```

You can read more about unapply attacks [here](https://glebbahmutov.com/blog/unapply-attack/).