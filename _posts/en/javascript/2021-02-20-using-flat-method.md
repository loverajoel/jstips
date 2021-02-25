---
layout: post

title: What is the flat method?
tip-number: 82
tip-username: katiie
tip-username-profile: https://github.com/katiie
tip-tldr: The flat method is used to flatten an array

categories:
    - en
    - javascript
---

The Flat operation creates a new array from an array with all sub-array elements concatenated into it recursively up to the specified depth.
This method can be used to flatten the records into one array.

```javascript
// Flattening arrays and objects
let arr1 = [["$6"], ["$12"], ["$25"], [["$18"]]]; 
let flattenedArray = arr1.flat();
console.log(flattenedArray);
// Output: [ $6, $12, $25, ["$18"] ] 

```javascript
flattenedArray = arr1.flat(2);
console.log(flattenedArray);
// Output: [ $6, $12, $25, $18 ] 

```javascript
```
