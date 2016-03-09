---
layout: post

title: Use destructuring in function parameters
tip-number: 43
tip-username: dislick 
tip-username-profile: https://github.com/dislick
tip-tldr: Did you know that you can use destructuring in function parameters?

categories:
    - en
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

Destructuring assignment with default parameters hides this to a certain extent:

```js
var sayHelloTimes2 = function({ name = "Anony", surname = "Moose" } = {}, times) {
  console.log(`Hello ${name} ${surname}! I've seen you ${times} times before.`);
};

sayHelloTimes({ name: "Pam" }, 5678)
// -> Hello Pam Moose! I've seen you 5678 times before.
sayHelloTimes2(5678)
// -> Hello Anony Moose! I've seen you undefined times before.
```

##### Availability

Note that destructuring assignment may not yet be available by default, in the version of Node.js or browser that you're using. For Node.js, you can try using the `--harmony-destructuring` flag on startup to activate this feature.
