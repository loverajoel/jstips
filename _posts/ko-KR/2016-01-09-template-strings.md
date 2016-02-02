---
layout: post

title: 템플릿 문자열(Template Strings)
tip-number: 09
tip-username: JakeRawr
tip-username-profile: https://github.com/JakeRawr
tip-tldr: ES6부터, JS는 기존 클래식, 따옴표 문자열 대신해 템플릿 문자열을 가진다.

categories:
    - ko
---
<translator: https://github.com/tisohjung>

ES6부터, JS는 기존 클래식, 따옴표 문자열 대신해 템플릿 문자열을 가진다.

예:
일반 문자열

```javascript
var firstName = 'Jake';
var lastName = 'Rawr';
console.log('My name is ' + firstName + ' ' + lastName);
// My name is Jake Rawr
```
템플릿 문자열

```javascript
var firstName = 'Jake';
var lastName = 'Rawr';
console.log(`My name is ${firstName} ${lastName}`);
// My name is Jake Rawr
```

템플릿 문자열에서 `\n` 없이 `${}` 안에 간단한 로직(ie 2+3)으로 여러 줄의 문자열을 할 수 있다.

또한 템플릿 문자열의 출력물을 함수를 이용해 변형 시킬 수 있다; [tagged template strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings#Tagged_template_strings) 에서 예제를 볼 수 있다.

[템플릿 문자열에 대해 더 알고 싶다면](https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2).