---
layout: post

title: Use destructuring in function parameters
tip-number: 43
tip-username: dislick 
tip-username-profile: https://github.com/dislick
tip-tldr: Did you know that you can use destructuring in function parameters?

redirect_from:
  - /en/use-destructuring-in-function-parameters/

categories:
    - en
    - javascript
---

I am sure many of you are already familiar with the [ES6 Destructuring Assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment). Did you know that you can also use it in function parameters? 

```js
var sayHello = function({ name, surname }) {
  console.log(`Hello ${name} ${surname}! How are you?`);
};

sayHello({ name: 'John', surname: 'Smith' })
// -> Hello John Smith! How are you?
```

This is great for functions which accept an options object. For this use case, you can also add [default parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters) to fill in whatever values the caller leaves out, or if the caller forgets to pass one at all:

```js
var sayHello2 = function({ name = "Anony", surname = "Moose" } = {}) {
  console.log(`Hello ${name} ${surname}! How are you?`);
};
```

The `= {}` says that the default object to be destructured for this parameter is `{}`, in case the caller forgets to pass the parameter, or passes one of the wrong type (more on this below).

```js
sayHello2()
// -> Hello Anony Moose! How are you?
sayHello2({ name: "Bull" })
// -> Hello Bull Moose! How are you?
```

##### Argument Handling

With plain destructuring assignment, if the the input parameter can't be matched with the function's specified object arguments, all the unmatched arguments are `undefined`, so you need to add code that handles this properly:

```js
var sayHelloTimes = function({ name, surname }, times) {
  console.log(`Hello ${name} ${surname}! I've seen you ${times} times before.`);
}

sayHelloTimes({ name: "Pam" }, 5678)
// -> Hello Pam undefined! I've seen you 5678 times before.
sayHelloTimes(5678)
// -> Hello undefined undefined! I've seen you undefined times before.
```

Worse, if the parameter to be destructured is missing, an exception is thrown, probably bringing your app to a screeching halt:

```js
sayHelloTimes()
// -> Uncaught TypeError: Cannot match against 'undefined' or 'null'...
```

It's conceptually similar to accessing a property of an undefined object, just with a different exception type.

Destructuring assignment with default parameters hides all the above to a certain extent:

```js
var sayHelloTimes2 = function({ name = "Anony", surname = "Moose" } = {}, times) {
  console.log(`Hello ${name} ${surname}! I've seen you ${times} times before.`);
};

sayHelloTimes2({ name: "Pam" }, 5678)
// -> Hello Pam Moose! I've seen you 5678 times before.
sayHelloTimes2(5678)
// -> Hello Anony Moose! I've seen you undefined times before.
sayHelloTimes2()
// -> Hello Anony Moose! I've seen you undefined times before.
```

As for `= {}`, it covers the case of a missing _object_, for which individual property defaults won't help at all:

```js
var sayHelloTimes2a = function({ name = "Anony", surname = "Moose" }, times) {
  console.log(`Hello ${name} ${surname}! I've seen you ${times} times before.`);
};

sayHelloTimes2a({ name: "Pam" }, 5678)
// -> Hello Pam Moose! I've seen you 5678 times before.
sayHelloTimes2a(5678)
// -> Hello Anony Moose! I've seen you undefined times before.
sayHelloTimes2a()
// -> Uncaught TypeError: Cannot match against 'undefined' or 'null'.
```

##### Availability

Note that destructuring assignment may not yet be available by default, in the version of Node.js or browser that you're using. For Node.js, you can try using the `--harmony-destructuring` flag on startup to activate this feature.
