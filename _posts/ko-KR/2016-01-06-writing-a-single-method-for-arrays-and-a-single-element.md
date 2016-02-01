---
layout: post

title: 배열또는 하나의 변수를 받는 함수를 하나로 만들기
tip-number: 06
tip-username: mattfxyz
tip-username-profile: https://twitter.com/mattfxyz
tip-tldr: 여러개의 함수를 만들어 배열과 각각의 요소들을 관리하는것 보다, 둘다 관리 할 수 있는 함수 하나를 만들어라. 몇몇의 jQuery 함수들이 이런식으로 구현되어있다 (`css`는 selector을 이용해 모든것을 수정한다).

categories:
    - ko
---
<translator: https://github.com/tisohjung>

여러개의 함수를 만들어 배열과 각각의 요소들을 관리하는것 보다, 둘다 관리 할 수 있는 함수 하나를 만들어라. 몇몇의 jQuery 함수들이 이런식으로 구현되어있다 (`css`는 selector을 이용해 모든것을 수정한다).

일단은 concat을 이용해 일단은 배열 형식으로 만든다. `Array.concat`는 배열 또는 한개의 원소를 받을 수 있다.

```javascript
function printUpperCase(words) {
  var elements = [].concat(words);
  for (var i = 0; i < elements.length; i++) {
    console.log(elements[i].toUpperCase());
  }
}
```

`printUpperCase`는 이제 하나의 노드 또는 노드 배열을 파라미터 값으로 받을 수 있다.

```javascript
printUpperCase("cactus");
// => CACTUS
printUpperCase(["cactus", "bear", "potato"]);
// => CACTUS
//  BEAR
//  POTATO
```
