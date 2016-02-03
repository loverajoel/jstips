---
layout: post

title: 模板字符串
tip-number: 09
tip-username: JakeRawr
tip-username-profile: https://github.com/JakeRawr
tip-tldr: ES6中，JS现在有了引号拼接字符串的替代品，模板字符串。

categories:
    - zh_CN
---


ES6中，JS现在有了引号拼接字符串的替代品，模板字符串。

示例:
普通字符串
```javascript
var firstName = 'Jake';
var lastName = 'Rawr';
console.log('My name is ' + firstName + ' ' + lastName);
// My name is Jake Rawr
```

模板字符串
```javascript
var firstName = 'Jake';
var lastName = 'Rawr';
console.log(`My name is ${firstName} ${lastName}`);
// My name is Jake Rawr
```


在模板字符串中，你可以不用`\n`来生成多行字符串还可以在`${}`里做简单的逻辑运算（例如 2+3）。

你也可以使用方法修改模板字符串的输出内容；他们被称为[带标签的模板字符串](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/template_strings#Tagged_template_strings)（其中有带标签的模板字符串的示例）

或许你还想[阅读更多内容](https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2)来了解模板字符串。
