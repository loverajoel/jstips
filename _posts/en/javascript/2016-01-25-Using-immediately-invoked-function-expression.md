---
layout: post

title: Using immediately invoked function expression
tip-number: 25
tip-username: rishantagarwal 
tip-username-profile: https://github.com/rishantagarwal
tip-tldr: Called as "Iffy" ( IIFE - immediately invoked function expression) is an anonymous function expression that is immediately invoked and has some important uses in Javascript.


redirect_from:
  - /en/Using-immediately-invoked-function-expression/

categories:
    - en
    - javascript
---

Called as "Iffy" ( IIFE - immediately invoked function expression) is an anonymous function expression that is immediately invoked and has some important uses in Javascript.

```javascript

(function() {
 // Do something​
 }
)()

```

It is an anonymous function expression that is immediately invoked, and it has some particularly important uses in JavaScript.

The pair of parenthesis surrounding the anonymous function turns the anonymous function into a function expression or variable expression. So instead of a simple anonymous function in the global scope, or wherever it was defined, we now have an unnamed function expression.

Similarly, we can even create a named, immediately invoked function expression:

```javascript
(someNamedFunction = function(msg) {
	console.log(msg || "Nothing for today !!")
	}) (); // Output --> Nothing for today !!​
​
someNamedFunction("Javascript rocks !!"); // Output --> Javascript rocks !!
someNamedFunction(); // Output --> Nothing for today !!​
```

For more details, check the following URL's - 
1. [Link 1](https://blog.mariusschulz.com/2016/01/13/disassembling-javascripts-iife-syntax) 
2. [Link 2](http://javascriptissexy.com/12-simple-yet-powerful-javascript-tips/) 

Performance:
[jsPerf](http://jsperf.com/iife-with-call)