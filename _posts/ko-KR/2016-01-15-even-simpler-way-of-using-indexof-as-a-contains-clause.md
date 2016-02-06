---
layout: post

title: `indexOf`를 포함문으로 사용하는 더 쉬운 방법
tip-number: 15
tip-username: jhogoforbroke
tip-username-profile: https://twitter.com/jhogoforbroke
tip-tldr: JavaScript 는 기본적으로 아무런 메소드를 포함하고있지 않다. 배열에서 아이템이나 문자열 에서 포함된 문자열을 찾을때 이 방법을 사용할 수 있다.

categories:
    - ko
---
<translator: https://github.com/tisohjung>

JavaScript 는 기본적으로 아무런 메소드를 포함하고있지 않다. 배열에서 아이템이나 문자열에서 포함된 문자열을 찾을때 이 방법을 사용할 수 있다:

```javascript
var someText = 'javascript rules';
if (someText.indexOf('javascript') !== -1) {
}

// or
if (someText.indexOf('javascript') >= 0) {
}
```

하지만 이걸 보자 [Expressjs](https://github.com/strongloop/express) 코드 스니펫.

[examples/mvc/lib/boot.js](https://github.com/strongloop/express/blob/2f8ac6726fa20ab5b4a05c112c886752868ac8ce/examples/mvc/lib/boot.js#L26)


```javascript
for (var key in obj) {
  // "reserved" exports
  if (~['name', 'prefix', 'engine', 'before'].indexOf(key)) continue;
```

[lib/utils.js](https://github.com/strongloop/express/blob/2f8ac6726fa20ab5b4a05c112c886752868ac8ce/lib/utils.js#L93)


```javascript
exports.normalizeType = function(type){
  return ~type.indexOf('/')
    ? acceptParams(type)
    : { value: mime.lookup(type), params: {} };
};
```

[examples/web-service/index.js](https://github.com/strongloop/express/blob/2f8ac6726fa20ab5b4a05c112c886752868ac8ce/examples/web-service/index.js#L35)


```javascript
// key is invalid
if (!~apiKeys.indexOf(key)) return next(error(401, 'invalid api key'));
```

봐야될점은 [bitwise operator(비트단위 연산자)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators) **~**이다, "Bitwise operator는 바이너리 단위의 연산을 하지만 Javascript 숫자단위 값을 리턴한다."

Javascript에서 `-1`을 `0`으로 치환해주고, `0` 를 `false`로 바꿔준다:

```javascript
var someText = 'text';
!!~someText.indexOf('tex'); // someText contains "tex" - true
!~someText.indexOf('tex'); // someText NOT contains "tex" - false
~someText.indexOf('asd'); // someText doesn't contain "asd" - false
~someText.indexOf('ext'); // someText contains "ext" - true
```

### String.prototype.includes()

ES6 에서 [includes() method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes)를 소개했고 이걸로 문자열에 다른 문자가 포함되는지 확인할 수 있다:

```javascript
'something'.includes('thing'); // true
```

ECMAScript 2016 (ES7)로는 배열로 이런 기법도 사용할 수 있다:

```javascript
!!~[1, 2, 3].indexOf(1); // true
[1, 2, 3].includes(1); // true
```

**불행히도, Chrome, Firefox, Safari 9 이상, Edge 에서만 지원이된다; IE11 및 그이하에서는 안된다.**
**제거 가능한 환경에서 더 사용하기 좋다.**