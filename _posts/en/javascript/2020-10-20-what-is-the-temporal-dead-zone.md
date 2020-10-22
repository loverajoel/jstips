---
layout: post

title: What is the Temporal Dead Zone?
tip-number: 76
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: Temporal Dead Zone is a JavaScript behavior while using variables declared using `let` and `const` keywords.

categories:
    - en
    - javascript
---

Temporal Dead Zone is a JavaScript behavior while using variables declared using `let` and `const` keywords. Since the keywords are block-scoped, the variables declared these keywords could not be accessed before the declaration, and then you will have to witness where variables will be said to be `undefined`. 


```javascript
function myFunc(){
  console.log(greeting);
  var greeting = 'Hello World!'
};
myFunc(); // Output: undefined

function myFunc() {
  console.log(greeting);
  let greeting = 'Hello World!';
};
myFunc(); // Output: ReferenceError: greeting is not defined

function myFunc() {
  console.log(greeting);
  const greeting = 'Hello World!';
}
myFunc(); // Output: ReferenceError: greeting is not defined
```