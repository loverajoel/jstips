---
layout: post

title: 函数参数内使用解构
tip-number: 43
tip-username: dislick 
tip-username-profile: https://github.com/dislick
tip-tldr: 你知道在函数参数内也可以使用解构吗？

categories:
    - zh_CN
---

大家一定对[ES6解构赋值](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)非常熟悉。但是你知道在函数参数里也可以使用它吗？

```javascript
var sayHello = function({ name, surname }) {
  console.log(`Hello ${name} ${surname}! How are you?`);
};

sayHello({
  name: 'John',
  surname: 'Smith'
});
```

这对于接收可选参数的函数，是很棒的。

> 请注意解构赋值在Node.js和大部分浏览器中仍然不可用。但是想自己尝试的话可以在Node.js下使用`--harmony-destructuring`标记。