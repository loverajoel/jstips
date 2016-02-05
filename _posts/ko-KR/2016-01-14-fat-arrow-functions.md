---
layout: post

title: Fat Arrow Functions(굵은 화살표 함수,=>)
tip-number: 14
tip-username: pklinger
tip-username-profile: https://github.com/pklinger/
tip-tldr: ES6의 새로운 기능으로 소개된 fat arrow functions는 코드를 줄여주는 간편한 도구가 될 수 있다.

categories:
    - ko
---
<translator: https://github.com/tisohjung>

ES6의 새로운 기능으로 소개된 fat arrow functions는 코드를 줄여주는 간편한 도구가 될 수 있다. 이름은 'fat arrow'라고 불리는 `=>` 부호에서 따왔다. thin arrow라 불리는 `->`와는 다르다. 몇몇 개발자들은 이미 이 타입의 함수를 Haskell에 'lamda expressions'혹은 'anonymous functions'와 같이 다른 언어에서 접했을 것이다. 이 화살표 함수들은 함수 이름의 정의돼있지 않아 anoymouse(익명)이라고 불린다.

### 이점은 무엇인가?
* Syntax: 적은 줄의 코딩; `function` 키워드를 또쓰고 쓸 필요 없다.
* Semantics(의미): `this` 키워드를 주변 문맥에서 받아온다

### 간단한 syntax 예제
아래 같은 일을 하는 두개의 코드를 보면 금방 fat arrow functions가 무슨 일을 하는지 알 수 있다:

```javascript
// general syntax for fat arrow functions
param => expression

// may also be written with parentheses
// parentheses are required on multiple params
(param1 [, param2]) => expression


// using functions
var arr = [5,3,2,9,1];
var arrFunc = arr.map(function(x) {
  return x * x;
});
console.log(arr)

// using fat arrow
var arr = [5,3,2,9,1];
var arrFunc = arr.map((x) => x*x);
console.log(arr)
```

보는 바와 같이 위 같은 경우에 fat arrow function이 괄호, 함수, 반환에 대한 타이핑과 시간을 줄여줄 것이다. 괄호는 `(x,y) => x+y`같은 다중 입력값에 필요한데, 필자는 그냥 모든 입력값에 괄호를 쓰기를 권한다. 실수를 예방하기 위함이다. 하지만 위에서 `x => x*x`와 같이 써도 무방하다. 지금까지 더 적은 줄의 코딩과 더 나은 가독성을 위한 구문 개선이다.

### `this`의 어휘적인 바인딩

fat arrow functions를 써야하는 또다는 이유가 있다. `this`의 맥락에 문제가 있다. fat arrow function은 `this`를 주변 문맥을 참고해서 선택하기 때문에 `bind(this)` 또는 `that = this`와 같은것에 대한 걱정을 할 필요가 없다. 다음 예제를 참고하자 [jsfiddle](https://jsfiddle.net/pklinger/rw94oc11/):

```javascript

// globally defined this.i
this.i = 100;

var counterA = new CounterA();
var counterB = new CounterB();
var counterC = new CounterC();
var counterD = new CounterD();

// bad example
function CounterA() {
  // CounterA's `this` instance (!! gets ignored here)
  this.i = 0;
  setInterval(function () {
    // `this` refers to global object, not to CounterA's `this`
    // therefore starts counting with 100, not with 0 (local this.i)
    this.i++;
    document.getElementById("counterA").innerHTML = this.i;
  }, 500);
}

// manually binding that = this
function CounterB() {
  this.i = 0;
  var that = this;
  setInterval(function() {
    that.i++;
    document.getElementById("counterB").innerHTML = that.i;
  }, 500);
}

// using .bind(this)
function CounterC() {
  this.i = 0;
  setInterval(function() {
    this.i++;
    document.getElementById("counterC").innerHTML = this.i;
  }.bind(this), 500);
}

// fat arrow function
function CounterD() {
  this.i = 0;
  setInterval(() => {
    this.i++;
    document.getElementById("counterD").innerHTML = this.i;
  }, 500);
}
```

Fat arrow functions에 대한 더 많은 정보는 여기서 찾을 수 있다 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions). 또다른 syntax 옵션을 보려면 [이곳](http://jsrocks.org/2014/10/arrow-functions-and-their-scope/)을 참고하자 