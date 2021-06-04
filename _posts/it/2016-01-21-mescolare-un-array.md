---
layout: post

titolo: Mescolare un Array
tip-numero: 21
tip-username: 0xmtn
tip-username-profile: https://github.com/0xmtn/
tip-tldr: Fisher-Yates Shuffling è un algoritmo per mescolare un array.

categoria:
    - it
---

 Questo frammento di codice utilizza l'algoritmo [Fisher-Yates Shuffling](https://www.wikiwand.com/en/Fisher%E2%80%93Yates_shuffle) per mescolare un array.

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
Un esempio:

```javascript
var a = [1, 2, 3, 4, 5, 6, 7, 8];
var b = shuffle(a);
console.log(b);
// [2, 7, 8, 6, 5, 3, 1, 4]
```
