---
layout: post

title: 对数组洗牌
tip-number: 21
tip-username: 0xmtn
tip-username-profile: https://github.com/0xmtn/
tip-tldr: Fisher-Yates Shuffling 算法对数组进行洗牌

redirect_from:
  - /zh_cn/shuffle-an-array/

categories:
    - zh_CN
    - javascript
---

 
 这段代码运用了[Fisher-Yates Shuffling](https://www.wikiwand.com/en/Fisher%E2%80%93Yates_shuffle)算法对数组进行洗牌。
  
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

调用示例:

```javascript
var a = [1, 2, 3, 4, 5, 6, 7, 8];
var b = shuffle(a);
console.log(b);
// [2, 7, 8, 6, 5, 3, 1, 4]
```
