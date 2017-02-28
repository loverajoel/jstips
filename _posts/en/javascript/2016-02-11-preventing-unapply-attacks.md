---
layout: post

title: Preventing Unapply Attacks
tip-number: 42
tip-username: emars 
tip-username-profile: https://twitter.com/marseltov
tip-tldr: Freeze the builtin prototypes.

redirect_from:
  - /en/preventing-unapply-attacks/

categories:
    - en
    - javascript
---

By overriding the builtin prototypes, external code can cause code to break by rewriting code to expose and change bound arguments. This can be an issue that seriously breaks applications that works by using polyfill es5 methods.

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
Although this concept is called an 'unapply attack' due to some code being able to access closures that normally wouldn't be in scope, it is mostly wrong to consider this a security feature due to it not preventing an attacker with code execution from extending prototypes before the freezing happens and also still having the potential to read all scopes using various language features. ECMA modules would give realm based isolation which is much stronger than this solution however still doesn't fix the issues of third party scripts.
