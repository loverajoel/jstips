---
layout: post

title: 배열 섞기
tip-number: 21
tip-username: 0xmtn
tip-username-profile: https://github.com/0xmtn/
tip-tldr: Fisher-Yates Shuffling 은 배열을 섞기 위한 알고리즘이다.

categories:
    - ko
---
<translator: https://github.com/tisohjung>

여기 사용된 예제는 [Fisher-Yates Shuffling](https://www.wikiwand.com/en/Fisher%E2%80%93Yates_shuffle) 알고리즘을 이용해 배열을 섞는다.

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
예제:

```javascript
var a = [1, 2, 3, 4, 5, 6, 7, 8];
var b = shuffle(a);
console.log(b);
// [2, 7, 8, 6, 5, 3, 1, 4]
```