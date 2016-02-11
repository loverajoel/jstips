---
layout: post

title: 반올림 빠르게 하기
tip-number: 18
tip-username: pklinger
tip-username-profile: https://github.com/pklinger
tip-tldr: 오늘의 팁은 성능에 대해서이다. 쌍물결(double tilde) 연산 `~~`을 본적이있는가? 더블 NOT bitwise operator이라고도 불린다. `Math.floor()`을 대신해 쓸수있다. 왜일까?

categories:
    - ko
---
<translator: https://github.com/tisohjung>

오늘의 팁은 성능에 대해서이다. 쌍물결(double tilde) 연산 `~~`을 본적이있는가? 더블 NOT bitwise operator이라고도 불린다. `Math.floor()`을 대신해 쓸수있다. 왜일까?

한개의 물결`~`은 32비트 변환된 입력을 `-(input+1)`으로 바꿔준다. 때문에 더블 비트단위 쉬프트는 입력값을 `-(-(input + 1)+1)`으로 변환해줘서 0으로 가깝에 반올림을 해준다. 때문에 숫자 입력값은 음수일때 `Math.ceil()`, 양수일때 `Math.floor()`이 된다. 실패시 `0`이 반환되서 때때로 `NaN`을 반환하는 `Math.floor()`보다 편리하다.

```javascript
// single ~
console.log(~1337)    // -1338

// numeric input
console.log(~~47.11)  // -> 47
console.log(~~-12.88) // -> -12
console.log(~~1.9999) // -> 1
console.log(~~3)      // -> 3

// on failure
console.log(~~[]) // -> 0
console.log(~~NaN)  // -> 0
console.log(~~null) // -> 0

// greater than 32 bit integer fails
console.log(~~(2147483647 + 1) === (2147483647 + 1)) // -> 0
```

`~~`가 성능적으로 더 좋을지라도, 접근성을 위해서는 `Math.floor()`을 사용하자.