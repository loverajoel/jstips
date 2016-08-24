---
layout: post

title: Tilde(~) operator in JS
tip-number: xx
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: Tilde(~) is a unary operator that takes an expression( say N ) on its right and converts it to -(N+1).

categories:
- en
---
Tilde is a unary operator, which takes an expression on its right(for instance N) and converts it to -(N+1).
Example:-
```js
console.log(~2);    //-3 
console.log(~1);    //-2 
console.log(~0);    //-1 
console.log(~-1);    //0 
console.log(~-2);    //1 
```
Unless we actually have an application that needs to run this algorithm on numbers, how are we going to use this squiggly little character to our advantage?

Functions like `indexOf` returns -1 when the query is not found. We saw above that ~ on -1 converts it to 0. The number 0 is a falsy value, meaning that it will evaluate to false when converted to a Boolean.

So, instead of writing something similar to this:
```js
var str = "hello";
if(str.indexOf("hello") >= 0){
  console.log("Its a hello");
}else{
  console.log("Not found.");
}
```
You can now have fewer characters in your code so you can write it like this:
```js
var str = "hello";
if(~str.indexOf("hello")){
  console.log("Its a hello");
}else{
  console.log("Not found.");
}
```
