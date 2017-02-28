---
layout: post

title: Implementing asynchronous loop
tip-number: 34
tip-username: madmantalking
tip-username-profile: https://github.com/madmantalking
tip-tldr: You may run into problems while implementing asynchronous loops. 

redirect_from:
  - /en/implementing-asynchronous-loops/

categories:
    - en
    - javascript
---

Let's try out writing an asynchronous function which prints the value of the loop index every second.

```js
for (var i=0; i<5; i++) {
	setTimeout(function(){
		console.log(i); 
	}, 1000 * (i+1));
}  
```
The output of the above programs turns out to be

```js
> 5
> 5
> 5
> 5
> 5
```
So this definitely doesn't work.

**Reason**

Each timeout refers to the original `i`, not a copy. So the for loop increments `i` until it gets to 5, then the timeouts run and use the current value of `i` (which is 5).

Well , this problem seems easy. An immediate solution that strikes is to cache the loop index in a temporary variable.

```js
for (var i=0; i<5; i++) {
	var temp = i;
 	setTimeout(function(){
		console.log(temp); 
	}, 1000 * (i+1));
}  
```
But again the output of the above programs turns out to be

```js
> 4
> 4
> 4
> 4
> 4
```

So , that doesn't work either , because blocks don't create a scope and variables initializers are hoisted to the top of the scope. In fact, the previous block is the same as:

```js
var temp;
for (var i=0; i<5; i++) {
 	temp = i;
	setTimeout(function(){
		console.log(temp); 
  	}, 1000 * (i+1));
}  
```
**Solution**

There are a few different ways to copy `i`. The most common way is creating a closure by declaring a function and passing `i` as an argument. Here we do this as a self-calling function.

```js
for (var i=0; i<5; i++) {
	(function(num){
		setTimeout(function(){
			console.log(num); 
		}, 1000 * (i+1)); 
	})(i);  
}  
```
In JavaScript, arguments are passed by value to a function. So primitive types like numbers, dates, and strings are basically copied. If you change them inside the function, it does not affect the outside scope. Objects are special: if the inside function changes a property, the change is reflected in all scopes.

Another approach for this would be with using `let`. With ES6 the `let` keyword is useful since it's block scoped unlike `var`

```js
for (let i=0; i<5; i++) {
 	setTimeout(function(){
		console.log(i); 
	}, 1000 * (i+1));
}  
```
