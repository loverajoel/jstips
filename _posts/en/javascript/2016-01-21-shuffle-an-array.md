---
layout: post

title: Shuffle an Array
tip-number: 21
tip-username: 0xmtn
tip-username-profile: https://github.com/0xmtn/
tip-tldr: Fisher-Yates Shuffling it's an algorithm to shuffle an array.

redirect_from:
  - /en/shuffle-an-array/

categories:
    - en
    - javascript
---

 This snippet here uses [Fisher-Yates Shuffling](https://www.wikiwand.com/en/Fisher%E2%80%93Yates_shuffle) Algorithm to shuffle a given array.

```javascript
function shuffle(arr) {
    var i,
        j,
        temp;
    for (i = arr.length - 1; i > 0; i--) {
        j = Math.floor(Math.random() * (i + 1));
        temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
    return arr;    
};
```
An example:

```javascript
var a = [1, 2, 3, 4, 5, 6, 7, 8];
var b = shuffle(a);
console.log(b);
// [2, 7, 8, 6, 5, 3, 1, 4]
```