---
layout: post

title: ES6 Destructuring
tip-number: 26
tip-username: webb04
tip-username-profile: https://github.com/webb04
tip-tldr: ES6 destructuring is a syntax modernization that improves readability and reduces the amount of code necessary for expressive declarations.

categories:
    - en
---

ES6 destructuring is a syntax modernization that improves readability and reduces the amount of code necessary for expressive declarations.

### Array destructuring

```javascript
// access first three items in an Array
const someArray = [1,2,3];
const [first, second, third] = someArray;

// possible to skip over elements
const [,,third] = ["el1", "el2", "el3"];
console.log(third);
// "el3"

// capture the remaining elements using the ES6 "rest" pattern
const [head, body, ...tail] = [1, 2, 3, 4];
console.log(tail);
// [3, 4]

// nice way to swap variables
let first = 1;
let second = 2;
[first, second] = [second, first];

// nice way to return a tuple from a function
function tuple() {
  return [1, 2];
}

const [first, second] = tuple();
 ```

### Object destructuring

 ```javascript
 // bind property to a constant
 const personA = { name: "foo" };
 const personB = { name: "bar" };

 const { name: nameA } = personA;
 const { name: nameB } = personB;

 console.log(nameA);
 // "foo"
 console.log(nameB);
 // "bar"

// shortcut for when property and variable names are the same
 let { foo, bar } = { foo: "first", bar: "second" };
 console.log(foo);
 // "first"
 console.log(bar);
 // "second"

 // you can specify default values
 const {firstName = "John", lastName: surname = "Doe"} = {};
  ```

You can find more information about JavaScript ES6 destructuring here:
* [Getting Started with JavaScript ES6 Destructuring](https://strongloop.com/strongblog/getting-started-with-javascript-es6-destructuring/)
* [ES6 In Depth: Destructuring](https://hacks.mozilla.org/2015/05/es6-in-depth-destructuring/)
