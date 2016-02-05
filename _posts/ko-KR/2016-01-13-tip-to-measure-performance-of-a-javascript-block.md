---
layout: post

title: 자바스크립트 블럭 선능 측정 팁
tip-number: 13
tip-username: manmadareddy
tip-username-profile: https://twitter.com/manmadareddy
tip-tldr: 간단히 자바스크립트 블록 성능 측정을 하기 위해, `console.time(label)`과 `console.timeEnd(label)`같은 콘솔 함수를 사용할 수 있다.

categories:
    - ko
---
<translator: https://github.com/tisohjung>

간단히 자바스크립트 블록 성능 측정을 하기 위해, [`console.time(label)`](https://developer.chrome.com/devtools/docs/console-api#consoletimelabel)과 [`console.timeEnd(label)`](https://developer.chrome.com/devtools/docs/console-api#consoletimeendlabel)같은 콘솔 함수를 사용할 수 있다.

```javascript
console.time("Array initialize");
var arr = new Array(100),
    len = arr.length,
    i;

for (i = 0; i < len; i++) {
    arr[i] = new Object();
};
console.timeEnd("Array initialize"); // Outputs: Array initialize: 0.711ms
```

더 많은 정보:
[콘솔 객체](https://github.com/DeveloperToolsWG/console-object),
[자바스크립트 벤치마킹](https://mathiasbynens.be/notes/javascript-benchmarking)

데모: [jsfiddle](https://jsfiddle.net/meottb62/) - [codepen](http://codepen.io/anon/pen/JGJPoa) (브라우저 콘솔에 출력함)