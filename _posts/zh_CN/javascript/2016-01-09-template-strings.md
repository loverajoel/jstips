---
layout: post

title: 模板字符串
tip-number: 09
tip-username: JakeRawr
tip-username-profile: https://github.com/JakeRawr
tip-tldr: ES6中，JS现在有了引号拼接字符串的替代品，模板字符串。

redirect_from:
  - /zh_cn/template-strings/

categories:
    - zh_CN
    - javascript
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

在模板字符串中，你可以不用`\n`来生成多行字符串，在`${}`里做简单的逻辑运算（例如 2+3）甚至使用[逻辑运算符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)。

```javascript
var val1 = 1, val2 = 2;
console.log(`${val1} is ${val1 < val2 ? 'less than': 'greater than'} ${val2}`)
// 1 is less than 2
```

你也可以使用函数修改末班字符串的输出内容；这被称为[带标签的模板字符串](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/template_strings#带标签的模板字符串)，其中包含了带标签的模板字符串的示例.


或许你还想[阅读更多内容](https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2)来了解模板字符串。
