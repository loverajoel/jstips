---
layout: post

title: == 대신 === 를 사용하라
tip-number: 24
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: `==` (혹은 `!=`) 연산자는 필요시 자동 형변환을 시행한다. `===` (혹은 `!==`) 연산자는 아무런 타입 변환도 하지 않는다. 값과 형에대한 비교를 하며 `==`보다 더 빠르다고 여겨진다. ([jsPref](http://jsperf.com/strictcompare))

categories:
    - ko
---
<translator: https://github.com/tisohjung>

`==` (혹은 `!=`) 연산자는 필요시 자동 형변환을 시행한다. `===` (혹은 `!==`) 연산자는 아무런 타입 변환도 하지 않는다. 값과 형에대한 비교를 하며 `==`보다 더 빠르다고 여겨진다. ([jsPref](http://jsperf.com/strictcompare))

```js
[10] ==  10      // is true
[10] === 10      // is false

'10' ==  10      // is true
'10' === 10      // is false

 []  ==  0       // is true
 []  === 0       // is false

 ''  ==  false   // is true but true == "a" is false
 ''  === false   // is false 

```
