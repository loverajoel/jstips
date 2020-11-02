---
layout: post

title: What is a spread operator?
tip-number: 78
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: The spread operator is a useful syntax for manipulating arrays and objects.

categories:
    - en
    - javascript
---
The spread operator is a useful syntax for adding items to arrays, combining arrays or objects, and spreading an array into a function’s arguments.

```js
// Concatenating arrays and objects
let arr = [1,2,3]; 
let arr2 = [4,5]; 
let arr = [...arr,...arr2]; 
console.log(arr);
// Output: [ 1, 2, 3, 4, 5 ] 

// Copying array elements
let arr = ['a','b','c']; 
let arr2 = [...arr]; 
console.log(arr);
// Output: ['a','b','c']

// Expanding arrays
let arr = ['a','b']; 
let arr2 = [...arr,'c','d']; 
console.log(arr);
// Output: ['a','b','c', 'd']

// Merging objects
const userBasic = { 
	name: 'Jen', 
	age: 22,
}; 
const userMoreInfo = { 
	country: 'Argentina', 
	city: 'Córdoba', 
}; 
const user = {... userBasic, ... userMoreInfo};
// Output: {  name: 'Julio',  age: 22, country: 'Argentina', city: 'Córdoba' }
```