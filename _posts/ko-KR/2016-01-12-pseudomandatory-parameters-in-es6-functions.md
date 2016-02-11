---
layout: post

title: ES6 함수의 의사필수(Pseudomandatory) 매개 변수
tip-number: 12
tip-username: Avraam Mavridis
tip-username-profile: https://github.com/AvraamMavridis
tip-tldr: 많은 프로그래밍 언어에서 함수의 매개 변수는 거의 필수다, 그리고 개발자는 매개 변수가 선택적이라고 명시적으로 정의 해야한다.

categories:
    - ko
---
<translator: https://github.com/tisohjung>

많은 프로그래밍 언어에서 함수의 매개 변수는 거의 필수고 개발자는 매개 변수가 선택적이라고 명시적으로 정의해야 한다. 자바스크립트에서는 모든 매개변수가 선택적이다, 하지만 우리는 함수 바디를 더럽히지 않고도, [**ES6의 매개변수를 위한 기본 값**](http://exploringjs.com/es6/ch_parameter-handling.html#sec_parameter-default-values)을 이용해, 이러한 기능을 적용할 수 있다.

```javascript
const _err = function( message ){
  throw new Error( message );
}

const getSum = (a = _err('a is not defined'), b = _err('b is not defined')) => a + b

getSum( 10 ) // throws Error, b is not defined
getSum( undefined, 10 ) // throws Error, a is not defined
 ```

`_err`는 즉시 Error을 던져주는 함수이다. 매개변수에 아무런 값을 넘겨주지 않았다면 기본값이 사용될 것이고, `_err`을 부를 것이다. **기본 매개 변수 기능**에 대한 더 많은 예제는 여기서 볼 수 있다 [Mozilla's Developer Network ](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/default_parameters).