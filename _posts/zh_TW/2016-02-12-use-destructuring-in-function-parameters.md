---
layout: post

title: 在函式參數裡使用解構子
tip-number: 43
tip-username: dislick
tip-username-profile: https://github.com/dislick
tip-tldr: 你知道可以在函式的參數裡使用解構子嗎？

categories:
    - zh_TW
---
我相信很多人都已經很熟悉 [ES6 解構賦值](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)。你知道也可以用在函式的參數裡嗎？

```javascript
var sayHello = function({ name, surname }) {
  console.log(`Hello ${name} ${surname}! How are you?`);
};

sayHello({
  name: 'John',
  surname: 'Smith'
});
```

這對函式接受一個可選的物件是相當有用的。

> 請注意解構賦值現在 Node.js 還有其他瀏覽器還無法使用。如果你想要試試看的話，你可以在 Node.js 使用 `--harmony-destructuring`。
