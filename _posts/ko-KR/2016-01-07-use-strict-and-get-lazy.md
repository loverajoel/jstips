---
layout: post

title: use strict를 사용하고 게을러지자
tip-number: 07
tip-username: nainslie
tip-username-profile: https://twitter.com/nat5an
tip-tldr: Strict-mode 자바스크립트는 개발자에게 안전한 자바스크립트를 더 쉽게 만들게 해준다.

categories:
    - ko
---
<translator: https://github.com/tisohjung>

Strict-mode 자바스크립트는 개발자에게 안전한 자바스크립트를 더 쉽게 만들게 해준다.

디폴트로 자바스크립트는 프로그래머가 쉽게 부주의 하게 만든다. 예를 들어, 처음에 소개할때 "var"을 사용하지 않고도 변수를 선언할 수 있게 소개한다. 노련한 개발자에게는 편리한것 처럼보이나, 타이핑 실수나 스코프밖에서 부르면서 많은 에러를 초래한다.

프로그래머는 우리를 위해 컴퓨터가 재루한 일들을 해주길 바라고 자동으로 실수를 수정해주길 바란다. 자바스크립트에 "use strict" 다이렉티브는 실수를 에러로 바꿔주면서 이 일을 해준다.

다이렉티브를 js파일의 제일 윗부분에 추가하거나:

```javascript
// Whole-script strict mode syntax
"use strict";
var v = "Hi!  I'm a strict mode script!";
```

함수 안에 추가한다:

```javascript
function f()
{
  // Function-level strict mode syntax
  'use strict';
  function nested() { return "And so am I!"; }
  return "Hi!  I'm a strict mode function!  " + nested();
}
function f2() { return "I'm not strict."; }
```

다이렉티브를 자바스크립트 파일이나 함수에 추가하면서, 자바스크립트 엔진에게 strict 모드로 실행하게 알려준다. 이로써 큰 자바스크립트 프로젝트에 항상 생기는 많은 의도치 않은 행동을 막아준다. 다른것보다, strict 모드는 다음과 같은 행동을 바꿔준다:

* 변수는 "var"로 미리 선언되었을때만 사용 할 수 있다.
* read-only 에다 쓰려고 할경우 noisy error을 만들어낸다.
* 생성자는 "new" 라는 키워드를 사용해 만들어야한다.
* "this"는 암시적으로 전역객체에 바인딩 되지 않는다.
* eval()은 아주 제한적으로 사용 가능하다.
* 이미 할당된 단어를 쓰거나 할당될 변수 이름에 대해 보호된다.

Strict 모드는 새로운 프로젝트에 아주 좋다. 하지만 이걸 쓰지 않은 이전 프로젝트에 도입하기에는 도전적일 수 있다. 또한 js 파일을 하나로 합쳐서 실행한다면, 모든 파일이 strict 모드로 실행될 수 있기에, 더 큰 문제가 생길 수 있다.

이건 앞선 자바스크립트에서 무시한 선언문이 아닌 일종의 문자 표현이다.
Strict 모드는 다음과 같은 환경에서 제공된다:

* Internet Explorer version 10 이상.
* Firefox version 4 이상.
* Chrome version 13 이상.
* Safari version 5.1 이상.
* Opera version 12 이상.

[MDN에 strict 모드에 대한 자세한 설명이 나와있다.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode).