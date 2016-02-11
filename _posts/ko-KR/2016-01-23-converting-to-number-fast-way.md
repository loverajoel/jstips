---
layout: post

title: 빠르게 숫자로 변환하기
tip-number: 23
tip-username: sonnyt
tip-username-profile: http://twitter.com/sonnyt
tip-tldr: 문자열을 숫자로 변환하는 일은 흔히있다. 가장 간단하고 빠른 방법은 + 연산자를 이용하는 것이다.

categories:
    - ko
---
<translator: https://github.com/tisohjung>

문자열을 숫자로 변환하는 일은 흔히있다. 가장 빠르고 간단한 방법은 `+`(더하기) 연산자를 이용하는 것이다. ([jsPref](https://jsperf.com/number-vs-parseint-vs-plus/29))

```javascript
var one = '1';

var numberOne = +one; // Number 1
```

다음과 같이 `-` (빼기) 연산자를 이용해 쉽게 음수로 변환 할 수도 있다.

```javascript
var one = '1';

var negativeNumberOne = -one; // Number -1
```