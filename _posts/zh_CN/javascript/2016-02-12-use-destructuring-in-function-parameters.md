---
layout: post

title: 函数参数内使用解构
tip-number: 43
tip-username: dislick 
tip-username-profile: https://github.com/dislick
tip-tldr: 你知道在函数参数内也可以使用解构吗？

redirect_from:
  - /zh_cn/use-destructuring-in-function-parameters/

categories:
    - zh_CN
    - javascript
---

大家一定对[ES6解构赋值](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)非常熟悉。但是你知道在函数参数里也可以使用它吗？

```js
var sayHello = function({ name, surname }) {
  console.log(`Hello ${name} ${surname}! How are you?`);
};

sayHello({ name: 'John', surname: 'Smith' })
// -> Hello John Smith! How are you?
```

这对于接收可选参数的函数，是很棒的。对于这种用法，你也可以添加[默认参数值](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Default_parameters)来填充调用者没有传递或忘记传递的参数值：

```js
var sayHello2 = function({ name = "Anony", surname = "Moose" } = {}) {
  console.log(`Hello ${name} ${surname}! How are you?`);
};
```

`= {}`表示此参数需要解构的默认对象是一个`{}`，以防调用者忘记传值，或传递了一个错误类型（大多情况为后者）。

```js
sayHello2()
// -> Hello Anony Moose! How are you?
sayHello2({ name: "Bull" })
// -> Hello Bull Moose! How are you?
```

##### 参数处理

对于普通的解构，如果输入的参数与函数指定的对象参数不符，所有不符的参数都将为`undefined`，所以你需要增加代码来正确的处理这些情况：

```js
var sayHelloTimes = function({ name, surname }, times) {
  console.log(`Hello ${name} ${surname}! I've seen you ${times} times before.`);
}

sayHelloTimes({ name: "Pam" }, 5678)
// -> Hello Pam undefined! I've seen you 5678 times before.
sayHelloTimes(5678)
// -> Hello undefined undefined! I've seen you undefined times before.
```

更糟糕的，如果没有传递需要解构的的参数，将会抛出错误，这可能使你的应用崩溃：

```js
sayHelloTimes()
// -> Uncaught TypeError: Cannot match against 'undefined' or 'null'...
```

这与访问一个未定义对象的参数基本相似，只是错误类型不太一样。

为解构增加默认参数基本上解决了上面的所有问题：

```js
var sayHelloTimes2 = function({ name = "Anony", surname = "Moose" } = {}, times) {
  console.log(`Hello ${name} ${surname}! I've seen you ${times} times before.`);
};

sayHelloTimes2({ name: "Pam" }, 5678)
// -> Hello Pam Moose! I've seen you 5678 times before.
sayHelloTimes2(5678)
// -> Hello Anony Moose! I've seen you undefined times before.
sayHelloTimes2()
// -> Hello Anony Moose! I've seen you undefined times before.
```

对于`= {}`，它掩盖了_object_未传递时的情况，但对于个别属性默认值的情形下会抛出异常：

```js
var sayHelloTimes2a = function({ name = "Anony", surname = "Moose" }, times) {
  console.log(`Hello ${name} ${surname}! I've seen you ${times} times before.`);
};

sayHelloTimes2a({ name: "Pam" }, 5678)
// -> Hello Pam Moose! I've seen you 5678 times before.
sayHelloTimes2a(5678)
// -> Hello Anony Moose! I've seen you undefined times before.
sayHelloTimes2a()
// -> Uncaught TypeError: Cannot match against 'undefined' or 'null'.
```

##### 可用性

需要注意解构赋值可能在你正在使用的Node.js或浏览器中默认情况下并不可用。对于Node.js，你可以在启动时使用`--harmony-destructuring`标记开启此特性。
