---
layout: post

title: 배열에 새로운 아이템 추가
tip-number: 00
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: 배열에 새로운 아이템을 추가하는 일은 일상적인 일이다. push를 이용해 배열의 끝, unshift로 배열의 처음, splice로 배열의 가운데에 추가 할 수 있다.

categories:
    - ko
---
<translator: https://github.com/tisohjung>

배열에 새로운 아이템을 추가하는 일은 일상적인 일이다. push를 이용해 배열의 끝, unshift로 배열의 처음, splice로 배열의 가운데에 추가 할 수 있다.

이게 가장 흔한 방법이지만 성능적으로 더 나은방법도 있다:

push()를 이용해 배열 끝에 요소를 추가하는것은 쉽다, 하지만 더 빠른 방법도있다.

```javascript
var arr = [1,2,3,4,5];

arr.push(6);
arr[arr.length] = 6; // 43% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
두 방법 다 기존의 배열을 수정한다. 링크 참조 [jsperf](http://jsperf.com/push-item-inside-an-array)

배열의 처음에 아이템을 추가할때:

```javascript
var arr = [1,2,3,4,5];

arr.unshift(0);
[0].concat(arr); // 98% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
더 자세한 팁 : unshift 는 개존 배열을 수정함; concat는 로운 배열을 반환함. [jsperf](http://jsperf.com/unshift-item-inside-an-array)

배열의 가운데 아이템을 추가하는건 splice를 이용하면 쉽다, 그리고 가장 빠른 방법이기도 하다.

```javascript
var items = ['one', 'two', 'three', 'four'];
items.splice(items.length / 2, 0, 'hello');
```

다양한 브라우저와 OS 에서 테스트 해본결과 비슷비슷했다. 위 테스트가 유용하기 바라며 스스로 꼭 테스트 해보길 바란다.