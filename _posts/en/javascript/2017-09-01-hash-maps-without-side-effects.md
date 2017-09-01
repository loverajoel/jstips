---
layout: post

title: Hash maps without side effects
tip-number: 73
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: Create hash maps(without side effects) using `Object.create(null)`.

categories:
    - en
    - javascript
---

# Hash maps without side effects

When you want to use javascript object as a hash map(purely for storing data), you might want to create it as follows.

```javascript
  const map = Object.create(null);
```

When creating a map using object literal(`const map = {}`), the map inherits properties from Object by default. It is equivalent to `Object.create(Object.prototype)`.

But by doing `Object.create(null)`, we explicitly specify `null` as its prototype. So it have absolutely no properties, not even constructor, toString, hasOwnProperty, etc. so you're free to use those keys in your data structure if you need to.

## Rationale:

```javascript
const dirtyMap = {};
const cleanMap = Object.create(null);

dirtyMap.constructor    // function Object() { [native code] }

cleanMap.constructor    // undefined

// Iterating maps

const key;
for(key in dirtyMap){
  if (dirtyMap.hasOwnProperty(key)) {   // Check to avoid iterating over inherited properties.
    console.log(key + " -> " + dirtyMap[key]);
  }
}

for(key in cleanMap){
  console.log(key + " -> " + cleanMap[key]);    // No need to add extra checks, as the object will always be clean
}
```

## Notes:
* Object.create() was introduced in ES5: [Compatibility](http://kangax.github.io/compat-table/es5/)
* ES6 introduced some new structures: [Map](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Map), [WeakMap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap), [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set) and [Weak Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakSet)
