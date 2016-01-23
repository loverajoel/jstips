---
layout: default
title: "Fat Arrow Functions #ES6"
author: "@pklinger"
author-link: https://github.com/pklinger/
---

Introduced as a new feature in ES6, fat arrow functions may come as a handy tool to write more code in less lines. The name comes from its syntax as `=>` is a 'fat arrow' compared to a thin arrow `->`. Some programmers might already know this type of functions from different languages such as Haskell as 'lambda expressions' respectively 'anonymous functions'. It is called anonymous, as these arrow functions do not have a descriptive function name.

### What are the benefits?
* Syntax: less LOC; no more typing `function` keyword over and over again
* Semantics: capturing the keyword `this` from the surrounding context

### Simple syntax example
Have a look at these two code snippets, which exactly do the same job. You will quickly understand what fat arrow functions do.

```javascript
// general syntax for fat arrow functions
param => expression

// may also be written with parentheses
// parentheses are required on multiple params
(param1 [, param2]) => expression


// using functions
var arr = [5,3,2,9,1];
var arrFunc = arr.map(function(x) {
  return x * x;
});
console.log(arr)

// using fat arrow
var arr = [5,3,2,9,1];
var arrFunc = arr.map((x) => x*x);
console.log(arr)
```

As you may see, the fat arrow function in this case may save you time typing out the parentheses as well as the function and return keywords. I would advice you to always write parentheses around the parameter inputs as the parentheses will be needed for multiple input parameters such as in `(x,y) => x+y` anyways. It is just a way to cope with forgetting them in different use cases. But the code above would also work like this: `x => x*x`. So far these are only syntactical improvements, which lead to less LOC and better readability.

### Lexically binding `this`

There is another good reason to use fat arrow functions. There is the issue with the context of `this`. With arrow functions, you will not worry about `.bind(this)` or setting `that = this` anymore, as fat arrow functions pick the context of `this` from the lexical surrounding. Have a look at the next [example] (https://jsfiddle.net/pklinger/rw94oc11/):

```javascript

// globally defined this.i
this.i = 100;

var counterA = new CounterA();
var counterB = new CounterB();
var counterC = new CounterC();
var counterD = new CounterD();

// bad example
function CounterA() {
  // CounterA's `this` instance (!! gets ignored here)
  this.i = 0;
  setInterval(function () {
    // `this` refers to global object, not to CounterA's `this`
    // therefore starts counting with 100, not with 0 (local this.i)
    this.i++;
    document.getElementById("counterA").innerHTML = this.i;
  }, 500);
}

// manually binding that = this
function CounterB() {
  this.i = 0;
  var that = this;
  setInterval(function() {
    that.i++;
    document.getElementById("counterB").innerHTML = that.i;
  }, 500);
}

// using .bind(this)
function CounterC() {
  this.i = 0;
  setInterval(function() {
    this.i++;
    document.getElementById("counterC").innerHTML = this.i;
  }.bind(this), 500);
}

// fat arrow function
function CounterD() {
  this.i = 0;
  setInterval(() => {
    this.i++;
    document.getElementById("counterD").innerHTML = this.i;
  }, 500);
}
```

Further information about fat arrow functions may be found at [MDN] (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions). To see different syntax options visit [this site] (http://jsrocks.org/2014/10/arrow-functions-and-their-scope/).
