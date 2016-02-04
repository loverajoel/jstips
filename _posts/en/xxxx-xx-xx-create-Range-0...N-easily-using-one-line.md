---
layout: post

title: Create Range 0...N easily using one line
tip-number: xx
tip-username: SarjuHansaliya
tip-username-profile: https://github.com/SarjuHansaliya
tip-tldr: We can create range function which will give 0...N range using one line only


categories:
    - en
---

Below is the line with which we can create 0...N range.

```js
Array.apply(null, {length: N}).map(Number.call, Number);
```

Lets break down this line into parts.We know how "call" function works in javascript.So in "call" first argument will be context and from second arguments , it will be list of arguments of function on which we are calling "call" function.

```js
function add(a,b){
    return (a+b);
}
add.call(null,5,6);
```
This will retun sun of 5 and 6.

map of array in javascript takes two arguments , first callback and second thisArg(context).Callback is taking three arguments , value , index and whole array on which we are iterating.so common syntax is like : 

```js
[1,2,3].map(function(val,index,arr){
    //Code
},this);
```
Below line create array of given length.

```js
Array.apply(null, {length: N})
```
Putting all parts together below is the solution.

```js
Array.apply(null, {length: N}).map(Number.call, Number);
```

If you want range 1...N , it will be like this.
```js
Array.apply(null, {length: N}).map(function(val,index){
  return index+1;  
});
```
