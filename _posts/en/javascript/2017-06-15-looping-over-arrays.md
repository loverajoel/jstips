---
layout: post

title: Looping over arrays
tip-number: 79
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: There's a few methods for looping over arrays in Javascript. We'll start with the classical ones and move towards additions made to the standard.

categories:
    - en
    - javascript
---

# Looping over arrays

There's a few methods for looping over arrays in Javascript. We'll start
with the classical ones and move towards additions made to the standard.

## while

```javascript
let index = 0;
const array = [1,2,3,4,5,6];

while (index < array.length) {
  console.log(array[index]);
  index++;
}
```

## for (classical)

```javascript
const array = [1,2,3,4,5,6];
for (let index = 0; index < array.length; index++) {
  console.log(array[index]);
}
```

## forEach

```javascript
const array = [1,2,3,4,5,6];

array.forEach(function(current_value, index, array) {
  console.log(`At index ${index} in array ${array} the value is ${current_value}`);
});
// => undefined
```

## map

The last construct was useful, however, it doesn't return a new array which might
be undesirable for your specific case. `map` solves this by applying a function
over every element and then returning the new array.

```javascript
const array = [1,2,3,4,5,6];
const square = x => Math.pow(x, 2);
const squares = array.map(square);
console.log(`Original array: ${array}`);
console.log(`Squared array: ${squares}`);
```

The full signature for `map` is `.map(current_value, index, array)`.

## reduce

From MDN:

> The reduce() method applies a function against an accumulator and each element
> in the array (from left to right) to reduce it to a single value.

```javascript
const array = [1,2,3,4,5,6];
const sum = (x, y) => x + y;
const array_sum = array.reduce(sum, 0);
console.log(`The sum of array: ${array} is ${array_sum}`);
```


## filter

Filters elements on an array based on a boolean function.

```javascript
const array = [1,2,3,4,5,6];
const even = x => x % 2 === 0;
const even_array = array.filter(even);
console.log(`Even numbers in array ${array}: ${even_array}`);
```

## every

Got an array and want to test if a given condition is met in every element?

```javascript
const array = [1,2,3,4,5,6];
const under_seven = x => x < 7;

if (array.every(under_seven)) {
  console.log('Every element in the array is less than 7');
} else {
  console.log('At least one element in the array was bigger than 7');
}
```

## some

Test if at least one element matches our boolean function.

```javascript
const array = [1,2,3,9,5,6,4];
const over_seven = x => x > 7;

if (array.some(over_seven)) {
  console.log('At least one element bigger than 7 was found');
} else {
  console.log('No element bigger than 7 was found');
}
```
