---
layout: post

title: Passing arguments to callback functions
tip-number: 16
tip-username: minhazav
tip-username-profile: https://twitter.com/minhazav
tip-tldr: By default you cannot pass arguments to a callback function, but you can take advantage of the closure scope in Javascript to pass arguments to callback functions.

redirect_from:
  - /en/passing-arguments-to-callback-functions/

categories:
    - en
    - javascript
---

By default you cannot pass arguments to a callback function. For example:

```js
function callback() {
  console.log('Hi human');
}

document.getElementById('someelem').addEventListener('click', callback);

```

You can take advantage of the closure scope in Javascript to pass arguments to callback functions. Check this example:

```js
function callback(a, b) {
  return function() {
    console.log('sum = ', (a+b));
  }
}

var x = 1, y = 2;
document.getElementById('someelem').addEventListener('click', callback(x, y));

```

### What are closures?

Closures are functions that refer to independent (free) variables. In other words, the function defined in the closure 'remembers' the environment in which it was created. [Check MDN Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) to learn more.

So this way the arguments `x` and `y` are in scope of the callback function when it is called.

Another method to do this is using the `bind` method. For example:

```js
var alertText = function(text) {
  alert(text);
};

document.getElementById('someelem').addEventListener('click', alertText.bind(this, 'hello'));
```
There is a very slight difference in performance of both methods, checkout [jsperf](http://jsperf.com/bind-vs-closure-23).
