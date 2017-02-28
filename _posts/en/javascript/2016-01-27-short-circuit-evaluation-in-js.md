---
layout: post

title: Short circuit evaluation in JS.
tip-number: 27
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: Short-circuit evaluation says, the second argument is executed or evaluated only if the first argument does not suffice to determine the value of the expression, when the first argument of the AND `&&` function evaluates to false, the overall value must be false, and when the first argument of the OR `||` function evaluates to true, the overall value must be true.

redirect_from:
  - /en/short-circuit-evaluation-in-js/

categories:
    - en
    - javascript
---

[Short-circuit evaluation](https://en.wikipedia.org/wiki/Short-circuit_evaluation) says, the second argument is executed or evaluated only if the first argument does not suffice to determine the value of the expression: when the first argument of the AND (`&&`) function evaluates to false, the overall value must be false; and when the first argument of the OR (`||`) function evaluates to true, the overall value must be true.

For the following `test` condition and `isTrue` and `isFalse` function.

```js
var test = true;
var isTrue = function(){
  console.log('Test is true.');
};
var isFalse = function(){
  console.log('Test is false.');
};

```
Using logical AND - `&&`.

```js
// A normal if statement.
if(test){
  isTrue();    // Test is true
}

// Above can be done using '&&' as -

( test && isTrue() );  // Test is true
```
Using logical OR - `||`.

```js
test = false;
if(!test){
  isFalse();    // Test is false.
}

( test || isFalse());  // Test is false.
```
The logical OR could also be used to set a default value for function argument.

```js
function theSameOldFoo(name){ 
  name = name || 'Bar' ;
  console.log("My best friend's name is " + name);
}
theSameOldFoo();  // My best friend's name is Bar
theSameOldFoo('Bhaskar');  // My best friend's name is Bhaskar
```
The logical AND could be used to avoid exceptions when using properties of undefined.
Example:

```js
var dog = { 
  bark: function(){
    console.log('Woof Woof');
  }
};

// Calling dog.bark();
dog.bark(); // Woof Woof.

// But if dog is not defined, dog.bark() will raise an error "Cannot read property 'bark' of undefined."
// To prevent this, we can use &&.

dog&&dog.bark();   // This will only call dog.bark(), if dog is defined.

```
