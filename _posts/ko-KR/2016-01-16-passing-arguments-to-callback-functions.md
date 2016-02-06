---
layout: post

title: 콜백함수에 인수 전달하기
tip-number: 16
tip-username: minhazav
tip-username-profile: https://twitter.com/minhazav
tip-tldr: JavaScript 모듈과 빌드 과정은 점점 더 많아지고 복잡해지고 있다, 하지만 boilerpalte와 새로운 프레임워크들은?

categories:
    - ko
---
<translator: https://github.com/tisohjung>

기본적으로 콜백함수에는 인수를 전달할 수 없다.
예를 들자면:

```js
function callback() {
  console.log('Hi human');
}

document.getElementById('someelem').addEventListener('click', callback);

```
클로져 스코프의 이점을 이용해 Javascript로 하여금 콜백 함수에 인수를 전달할 수 있다. 다음 예제를 확인해보자:
```js
function callback(a, b) {
  return function() {
    console.log('sum = ', (a+b));
  }
}

var x = 1, y = 2;
document.getElementById('someelem').addEventListener('click', callback(x, y));
```

### 클로져란 무엇인가?

클로저는 독립적인 (자유) 변수를 가리키는 함수이다. 또는, 클로저 안에 정의된 함수는 만들어진 환경을 '기억한다'.[MDN 도큐먼트 참조](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures).

그래서 인수 `x`와 `y`는 콜백 함수의 스코프 안에서 불리게된다.

다른 방법으로는 `bind`를 사용할 수 있다. 예제:

```js
var alertText = function(text) {
  alert(text);
};

document.getElementById('someelem').addEventListener('click', alertText.bind(this, 'hello'));
```
여기엔 성능면에서 미세한 차이가 있다. [jsperf](http://jsperf.com/bind-vs-closure-23) 참조.