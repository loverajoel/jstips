---
layout: post

title: 속성(property)이 객체(Object)인지 확인
tip-number: 10
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: 객체에 속성이 있는지 확인하는 몇가지 방법이다

categories:
    - ko
---
<translator: https://github.com/tisohjung>

[object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)에 속성이 있는지 확인해야 할때, 보통은 이런식으로 할것이다:

```javascript
var myObject = {
  name: '@tips_js'
};

if (myObject.name) { ... }

```

이것도 괜찮지만, 두가지 네이티브 방법이 있다. [`in` operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in)와 [`Object.hasOwnProperty`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty)이다. `Object`의 자식인 모든 객체는 두가지 방법이 다 가능하다.

### 두개의 차이를 보자

```javascript
var myObject = {
  name: '@tips_js'
};

myObject.hasOwnProperty('name'); // true
'name' in myObject; // true

myObject.hasOwnProperty('valueOf'); // false, valueOf is inherited from the prototype chain
'valueOf' in myObject; // true

```

둘은 속성을 얼마나 깊이 확인하는지 차이 있다. `hasOwnProperty`는 키값이 객체에 직접적으로 하위에 있을경우에만 참을 반환할 것이다. 하지만 `in`은 프로토타입 체인에서 가져온 모든 속성에 대해 참을 반환할 것이다.

또 다른 예제:

```javascript
var myFunc = function() {
  this.name = '@tips_js';
};
myFunc.prototype.age = '10 days';

var user = new myFunc();

user.hasOwnProperty('name'); // true
user.hasOwnProperty('age'); // false, because age is from the prototype chain
```

[실습 예제는 여기에](https://jsbin.com/tecoqa/edit?js,console)!

속성 유무 확인에 대해 자주 행하는 실수에 대해 [이 토론을 읽어 보는것을 추천한다](https://github.com/loverajoel/jstips/issues/62).