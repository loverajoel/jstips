---
layout: post

title: Template Strings
tip-number: 09
tip-username: JakeRawr
tip-username-profile: https://github.com/JakeRawr
tip-tldr: As of ES6, JS now has template strings as an alternative to the classic end quotes strings.

redirect_from:
  - /en/template-strings/

categories:
    - en
    - javascript
---

As of ES6, JS now has template strings as an alternative to the classic end quotes strings.

Ex:
Normal string

```javascript
var firstName = 'Jake';
var lastName = 'Rawr';
console.log('My name is ' + firstName + ' ' + lastName);
// My name is Jake Rawr
```
Template String

```javascript
var firstName = 'Jake';
var lastName = 'Rawr';
console.log(`My name is ${firstName} ${lastName}`);
// My name is Jake Rawr
```

You can do multi-line strings without `\n`, perform simple logic (ie 2+3) or even use the [ternary operator](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) inside `${}` in template strings.

```javascript
var val1 = 1, val2 = 2;
console.log(`${val1} is ${val1 < val2 ? 'less than': 'greater than'} ${val2}`)
// 1 is less than 2
```

You are also able to modify the output of template strings using a function; they are called [tagged template strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings#Tagged_template_strings) for example usages of tagged template strings.

You may also want to [read](https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2) to understand template strings more.
