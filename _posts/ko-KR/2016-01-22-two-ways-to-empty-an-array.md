---
layout: post

title: Two ways to empty an array
tip-number: 22
tip-username: microlv
tip-username-profile: https://github.com/microlv
tip-tldr: 자바스크립트에서 배열을 비우고 싶을때 다양한방법이 있지만 다음이 성능면에서 우월하다.

categories:
    - ko
---
<translator: https://github.com/tisohjung>

선언한 배열의 내용을 비우고 싶을때 보통은 이런식으로 한다:

```javascript
// define Array
var list = [1, 2, 3, 4];
function empty() {
    //empty your array
    list = [];
}
empty();
```
하지만 성능적인 면에서 더 나은 방법이 있다.

다음과 같은 코드를 이용한다:

```javascript
var list = [1, 2, 3, 4];
function empty() {
    //empty your array
    list.length = 0;
}
empty();
```

* `list = []`는 다른 참조값에 전혀 영향을 주지 않고, 새로운 배열을 할당해 참조한다.
그뜻은 이미 메모리에 올라와있던 배열은 메모리를 참조하며, 메모리 누수를 발생하고 있다는 소리다.

* `list.length = 0` 는 배열안에 모든것을 삭제한다, 그리고 다른 참조값에 영향을준다.
다시 말해서, 같은 배열에 대해 두개의 참조값이 있고 (`a = [1,2,3]; a2 = a;`), `list.length = 0`를 이용해 배열의 내용을 없앴다면, 둘다 (a와 a2) 빈 배열을 가르킬 것이라는 뜻이다. (a2의 배열을 유지하고 싶으면 이 방법을 사용하면 안된다!)

출력이 어떻게 될지 생각해보자:

```js
var foo = [1,2,3];
var bar = [1,2,3];
var foo2 = foo;
var bar2 = bar;
foo = [];
bar.length = 0;
console.log(foo, bar, foo2, bar2);

// [] [] [1, 2, 3] []
```

스택 오버플로우에 더 자세히 나와있다:
[difference-between-array-length-0-and-array](http://stackoverflow.com/questions/4804235/difference-between-array-length-0-and-array)
