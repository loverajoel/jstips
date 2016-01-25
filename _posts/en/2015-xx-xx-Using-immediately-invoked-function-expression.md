---
layout: post

title: Using immediately invoked function expression
tip-number: xx
tip-username: rishantagarwal 
tip-username-profile: https://github.com/rishantagarwal
tip-tldr: Called as "Iffy" ( IIFE - immediately invoked function expression) is an anonymous function expression that is immediately invoked and has some important uses in Javascript.


categories:
    - en
---

Called as "Iffy" ( IIFE - immediately invoked function expression) is an anonymous function expression that is immediately invoked and has some important uses in Javascript.

```javascript

(function () {
 // Do something​
 }
)()

```

It is an anonymous function expression that is immediately invoked, and it has some particularly important uses in JavaScript.

The pair of parenthesis surrounding the anonymous function turns the anonymous function into a function expression or variable expression. So instead of a simple anonymous function in the global scope, or wherever it was defined, we now have an unnamed function expression.

Similarly, we can even create a named, immediately invoked function expression:

```javascript
(someNamedFunction = function (msg) {
	console.log(msg || "Nothing for today !!")
	}) (); // Output --> Nothing for today !!​
​
someNamedFunction ("Javascript rocks !!"); // Output --> Javascript rocks !!
someNamedFunction (); // Output --> Nothing for today !!​
```

