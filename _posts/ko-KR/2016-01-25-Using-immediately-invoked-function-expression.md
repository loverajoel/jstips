---
layout: post

title: immediately invoked function expression (즉시 실행 함수) 사용하기
tip-number: 25
tip-username: rishantagarwal 
tip-username-profile: https://github.com/rishantagarwal
tip-tldr: Called as "Iffy" ( IIFE - immediately invoked function expression) is an anonymous function expression that is immediately invoked and has some important uses in Javascript.


categories:
    - ko
---
<translator: https://github.com/tisohjung>

"Iffy" ( IIFE - immediately invoked function expression) 라고도 불리는 익명의 함수 표현은 즉시 실행이되며 자바스크립트에서 중요하게 쓰인다.

```javascript

(function() {
 // Do something​
 }
)()

```

즉시 실행되는 익명의 함수이며, 자바스크립트에서 중요하게 쓰인다.

익명의 함수를 포괄하는 괄호는 함수를 함수 표현식 또는 변수 표현식으로 바꿔준다. 때문에 하나의 전역으로 정의하거나 할일 없이, 이름이 없는 함수 표현식이 만들어진다.

비슷한 방법으로 이름이 있는 immediately invoked function expression을 만들 수 있다:

```javascript
(someNamedFunction = function(msg) {
	console.log(msg || "Nothing for today !!")
	}) (); // Output --> Nothing for today !!​
​
someNamedFunction("Javascript rocks !!"); // Output --> Javascript rocks !!
someNamedFunction(); // Output --> Nothing for today !!​
```

더 자세한 정보를 위해 링크를 참조하자 - 
1. [Link 1](https://blog.mariusschulz.com/2016/01/13/disassembling-javascripts-iife-syntax) 
2. [Link 2](http://javascriptissexy.com/12-simple-yet-powerful-javascript-tips/) 

성능:
[jsPerf](http://jsperf.com/iife-with-call)