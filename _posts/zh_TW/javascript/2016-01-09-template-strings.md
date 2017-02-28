---
layout: post

title: 模板字串
tip-number: 09
tip-username: JakeRawr
tip-username-profile: https://github.com/JakeRawr
tip-tldr: 由於 ES6 中有了模板字串，JavaScript 可以使用模板字串來替代原本我們使用的引號字元。

redirect_from:
  - /zh_tw/template-strings/

categories:
    - zh_TW
    - javascript
---

由於 ES6 中有了模板字串，JavaScript 可以使用模板字串來替代原本我們使用的引號字元。

Ex:
正常的字串

```javascript
var firstName = 'Jake';
var lastName = 'Rawr';
console.log('My name is ' + firstName + ' ' + lastName);
// My name is Jake Rawr
```
模板字串

```javascript
var firstName = 'Jake';
var lastName = 'Rawr';
console.log(`My name is ${firstName} ${lastName}`);
// My name is Jake Rawr
```

在模板字串中，你不需要透過 `\n` 來產生多行的字串，只要簡單透過 `${}` 來替代就可以了，還可以計算簡單的邏輯，例如：`${2 + 3}`。
你也可以使用函式來修改你的輸出的內容；例如使用標籤模板字串，它們被稱為[標籤模板字串](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings#Tagged_template_strings)。

你或許想要[閱讀](https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2)和了解更多關於模板字串。
