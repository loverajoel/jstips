---
layout: post

title: Use destructuring in function parameters
tip-number: 43
tip-username: dislick 
tip-username-profile: https://github.com/dislick
tip-tldr: Did you know that you can use destructuring in function parameters?

categories:
    - en
---

I am sure many of you are already familiar with the [ES6 Destructuring Assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment). Did you know that you can also use it in function parameters? 

```javascript
var sayHello = function({ name, surname }) {
  console.log(`Hello ${name} ${surname}! How are you?`);
};

sayHello({
  name: 'John',
  surname: 'Smith'
});
```

This is great for functions which accept an options object.

> Please note that the Destructuring Assignment is not yet available in Node.js and almost all browsers. You can however use the `--harmony-destructuring` flag for Node.js if you'd like to try it for yourself now.