---
layout: post

title: Binding objects to functions
tip-number: 61
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: Understanding how to use `Bind` method with objects and functions in JavaScript


redirect_from:
  - /en/binding-objects-to-functions/

categories:
    - en
    - javascript
---

More than often, we need to bind an object to a function’s this object. JS uses the bind method when this is specified explicitly and we need to invoke desired method.

### Bind syntax

```js
fun.bind(thisArg[, arg1[, arg2[, ...]]])
```

## Parameters
**thisArg**

`this` parameter value to be passed to target function while calling the `bound` function.

**arg1, arg2, ...**

Prepended arguments to be passed to the `bound` function while invoking the target function.

**Return value**

A copy of the given function along with the specified `this` value and initial arguments.

### Bind method in action in JS

```js
const myCar = {
 brand: 'Ford',
 type: 'Sedan',
 color: 'Red'
};

const getBrand = function () {
 console.log(this.brand);
};

const getType = function () {
 console.log(this.type);
};

const getColor = function () {
 console.log(this.color);
};

getBrand(); // object not bind,undefined

getBrand(myCar); // object not bind,undefined

getType.bind(myCar)(); // Sedan

let boundGetColor = getColor.bind(myCar);
boundGetColor(); // Red

```