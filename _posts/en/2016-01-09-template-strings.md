---
layout: post

title: Template Strings
tip-number: 09
tip-username: JakeRawr
tip-username-profile: https://github.com/JakeRawr
tip-tldr: As of ES6, JS now has template strings as an alternative to the classic end quotes strings.

categories:
    - en
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

You can do multi-line strings without `\n` and simple logic (ie 2+3) inside `${}` in template strings.

You are also able to modify the output of template strings using a function; they are called [tagged template strings]
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings#Tagged_template_strings) for example usages of tagged template strings.

You may also want to [read](https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2) to understand template strings more.
