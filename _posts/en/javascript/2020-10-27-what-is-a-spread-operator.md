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
The spread operator in JavaScript is a useful syntax for adding elements to an array, combining arrays into one larger one, spreading an array inside the arguments of a function, and more.

```js
// Concatenating arrays and objects
let arr1 = [1,2,3]; 
let arr2 = [4,5]; 
let newArray = [...arr1,...arr2]; 
console.log(newArray);
// Output: [ 1, 2, 3, 4, 5 ] 

// Copying array elements
let arr = ["a","b","c"]; 
let newArray = [...arr]; 
console.log(newArray);
// Output: ["a", "b", "c"]

// Expanding arrays
let arr = ["a","b"]; 
let newArray = [...arr,"c","d"]; 
console.log(newArray);
// Output: ["a", "b", "c", "d"]

// Merging objects
const userBasic = { 
	name: "Jen", 
	age: 22,
}; 
const userMoreInfo = { 
	country: "Argentina", 
	city: "Córdoba", 
}; 
const user = {... userBasic, ... userMoreInfo};
// Output: {  name: "Jen",  age: 22, country: "Argentina", city: "Córdoba" }
```