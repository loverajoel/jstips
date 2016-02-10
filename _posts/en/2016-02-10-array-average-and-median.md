---
layout: post

title: Array average and median
tip-number: 41
tip-username: soyuka
tip-username-profile: https://github.com/soyuka
tip-tldr: Calculate the average and median from array values


categories:
    - en
---

The following examples will be based on the following array:

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
```

To get the average, we have to sum up numbers and then divide by the number of values. Steps are:
- get the array length
- sum up values
- get the average (`sum/length`)

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
let sum = values.reduce((previous, current) => current += previous);
let avg = sum / values.length;
// avg = 28
```

Or:

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
let count = values.length;
values = values.reduce((previous, current) => current += previous);
values /= count;
// avg = 28
```

Now, to get the median steps are:
- sort the array
- get the middle value

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
values.sort((a, b) => a - b);
let middle = Math.floor(values.length / 2);
let median = values[middle];
// median = 23
```

Or with a [right shift](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Right_shift) operator:

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
values.sort((a, b) => a - b);
let median = values[values.length >> 1];
// median = 23
```
