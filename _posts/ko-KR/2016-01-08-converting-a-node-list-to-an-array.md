---
layout: post

title: Converting a Node List to an Array
tip-number: 08
tip-username: Tevko
tip-username-profile: https://twitter.com/tevko
tip-tldr: Here's a quick, safe, and reusable way to convert a node list into an array of DOM elements.

categories:
    - ko
---
<translator: https://github.com/tisohjung>

`querySelectorAll` 함수는 노드 리스트라 불리는 array-like(배열같은) 객체를 반환한다. 데이터 구조는 "Array-like"라고도 한다, 배열 처럼 표현되기 때문이다. 하지만 배열의 함수인 `map`이나 `forEach`같은 곳에서는 사용 할 수 없다. 여기 노드 리스트를 DOM 요소로 이루어진 배열로 변환하는 빠르고, 안전하고, 재사용 가능한 방법이있다:

```javascript
const nodelist = document.querySelectorAll('div');
const nodelistToArray = Array.apply(null, nodelist);

//later on ..

nodelistToArray.forEach(...);
nodelistToArray.map(...);
nodelistToArray.slice(...);

//etc...
```

`apply` 메서드는 arguments의 배열과 주어진`this`값으로 함수를 호출한다.[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) 에는 `apply`가 array-like 객체를 갖는다고 명시되있다, 정확히 `querySelectorAll`의 환반과 같다. `this`값은 필수가 아니기 때문에, `null` 또는 `0`을 전달한다. 결과 값은 모든 배열 메서드를 포함하는 DOM 요소로 이루어진 배열이다.

혹은 ES2015를 사용한다면[spread operator `...`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)을 사용 할 수 있다.

```js
const nodelist = [...document.querySelectorAll('div')]; // returns a real array

//later on ..

nodelist.forEach(...);
nodelist.map(...);
nodelist.slice(...);

//etc...
```