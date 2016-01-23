---
layout: default
title: "Template Strings"
author: "@JakeRawr"
author-link: https://github.com/JakeRawr
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

You can do Multi-line strings without `\n` and simple logic (ie 2+3) inside `${}` in Template String.

You are also able to to modify the output of template strings using a function; they are called [Tagged template strings]
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings#Tagged_template_strings) for example usages of tagged template strings.

You may also want to [read](https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2) to understand template strings more
