---
layout: post

title: Avoid modifying or passing `arguments` into other functions — it kills optimization
tip-number: 31
tip-username: berkana
tip-username-profile: https://github.com/berkana
tip-tldr: Within JavaScript functions, the variable name `arguments` lets you access all of the arguments passed to the function. `arguments` is an *array-like object*; `arguments` can be accessed using array notation, and it has the *length* property, but it doesn't have many of the built-in methods that arrays have such as `filter` and `map` and `forEach`. Because of this, it is a fairly common practice to convert `arguments` into an array using the following snipet


redirect_from:
  - /en/avoid-modifying-or-passing-arguments-into-other-functions-it-kills-optimization/

categories:
    - en
    - javascript
---

###Background

Within JavaScript functions, the variable name [`arguments`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments) lets you access all of the arguments passed to the function. `arguments` is an *array-like object*; `arguments` can be accessed using array notation, and it has the *length* property, but it doesn't have many of the built-in methods that arrays have such as `filter` and `map` and `forEach`. Because of this, it is a fairly common practice to convert `arguments` into an array using the following:

```js
var args = Array.prototype.slice.call(arguments);
```
This calls the `slice` method from the `Array` prototype, passing it `arguments`; the `slice` method returns a shallow copy of `arguments` as a new array object. A common shorthand for this is :

```js
var args = [].slice.call(arguments);
```
In this case, instead of calling `slice` from the `Array` prototype, it is simply being called from an empty array literal.

###Optimization

Unfortunately, passing `arguments` into any function call will cause the V8 JavaScript engine used in Chrome and Node to skip optimization on the function that does this, which can result in considerably slower performance. See this article on [optimization killers](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers). Passing `arguments` to any other function is known as *leaking `arguments`*.

Instead, if you want an array of the arguments that lets you use you need to resort to this:

```js
var args = new Array(arguments.length);
for(var i = 0; i < args.length; ++i) {
  args[i] = arguments[i];
}
```

Yes it is more verbose, but in production code, it is worth it for the performance optimization.