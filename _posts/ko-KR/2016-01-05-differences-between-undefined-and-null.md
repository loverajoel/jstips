---
layout: post

title: `undefined` 과 `null`의 차이
tip-number: 05
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: `undefined` 과 `null`의 차이 이해.

categories:
    - ko
---
<translator: https://github.com/tisohjung>

- `undefined`는 변수가 아직 선언되지 않았거나, 선언되었지만 값이 할당되지 않았다는 뜻이다.
- `null` 은 "no value"즉 값이 없다는 할당값이다.
- 자바스크립트는 할당되지 않은 값들에 `undefined`를 기본으로 설정한다.
- 자바스크립트는 절대 `null`로 값을 설정하지 않는다. 프로그래머가 직접 `var` 에 값이 없다는 것을 명시할때만 사용된다.
- `undefined`는 JSON에 어 유효한 값이 아니지만 `null` 은 있다.
- `undefined`의 typeof 는 `undefined`이다.
- `null`의 typeof 는 `object`이다. [이유?](http://www.2ality.com/2013/10/typeof-null.html)
- 둘다 primitives(원시 데이터 타입)이다.
- 둘다 [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)이다(false값을 리턴).
  (`Boolean(undefined) // false`, `Boolean(null) // false`)
- 변수가 [undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined) 인지 확인 할 수 있다.

  ```javascript
  typeof variable === "undefined"
```
- 변수가 [null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null)인지 비교 할 수 있다.

  ```javascript
  variable === null
```
- **equality** 오퍼레이터가 같다고 표시하지만, **identity**는 다르다고 표시된다.

  ```javascript
  null == undefined // true

  null === undefined // false
```