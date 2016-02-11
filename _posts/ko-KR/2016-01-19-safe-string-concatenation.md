---
layout: post

title: 안전한 문자열의 연속
tip-number: 19
tip-username: gogainda
tip-username-profile: https://twitter.com/gogainda
tip-tldr: 하나의 문자열로 합치고 싶은, 타입을 모르는 몇개의 변수가 있다고 가정하자. 확실히 하기 위해 연결하는데 있어서 수학적인 연산은 들어가지 않는다, concat을 사용한다

categories:
    - ko
---
<translator: https://github.com/tisohjung>

하나의 문자열로 합치고 싶은, 타입을 모르는 몇개의 변수가 있다고 가정하자. 확실히 하기 위해 연결하는데 있어서 수학적인 연산은 들어가지 않는다, `concat`을 사용한다:

```javascript
var one = 1;
var two = 2;
var three = '3';

var result = ''.concat(one, two, three); //"123"
```

이러한 연결은 의도한바를 실행해준다. 반면, 더하기를 이용한 문자열의 연속은 의도치 않은 결과를 초래한다:

```javascript
var one = 1;
var two = 2;
var three = '3';

var result = one + two + three; //"33" instead of "123"
```

`join`[타입](http://www.sitepoint.com/javascript-fast-string-concatenation/)과 비교해 성능에 대해 예기하자면, `concat`과 비교해 별 차이나지 않는다.

`concat`에 대해 [MDN 페이지](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/concat)에서 더 알아볼 수 있다.