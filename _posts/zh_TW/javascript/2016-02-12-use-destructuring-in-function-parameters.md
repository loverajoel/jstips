---
layout: post

title: 在函式參數裡使用解構子
tip-number: 43
tip-username: dislick
tip-username-profile: https://github.com/dislick
tip-tldr: 你知道可以在函式的參數裡使用解構子嗎？

redirect_from:
  - /zh_tw/use-destructuring-in-function-parameters/

categories:
    - zh_TW
    - javascript
---

我相信很多人都已經很熟悉 [ES6 解構賦值](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)。你知道也可以用在函式的參數裡嗎？

```js
var sayHello = function({ name, surname }) {
  console.log(`Hello ${name} ${surname}! How are you?`);
};

sayHello({ name: 'John', surname: 'Smith' })
// -> Hello John Smith! How are you?
```

對函式來說可以接受一個可選擇的物件是非常有用的。對於這個使用方法，你可以加入[預設參數](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)來使用，不管是 caller 忘記賦值，或者是 caller 根本忘記傳送參數：

```js
var sayHello2 = function({ name = "Anony", surname = "Moose" } = {}) {
  console.log(`Hello ${name} ${surname}! How are you?`);
};
```

`= {}` 意思說預設物件可以被解構成這個 `{}` 參數，萬一 caller 忘記傳送參數，或傳送一個錯誤的類型（更多關於在下面）。

```js
sayHello2()
// -> Hello Anony Moose! How are you?
sayHello2({ name: "Bull" })
// -> Hello Bull Moose! How are you?
```

##### 參數處理

使用解構賦值，如果輸入參數不符合函式指定的物件參數，所有不符合的參數都是 `undefined`，所以你需要加入程式碼來正確的處理這些不符合的參數：

```js
var sayHelloTimes = function({ name, surname }, times) {
  console.log(`Hello ${name} ${surname}! I've seen you ${times} times before.`);
}

sayHelloTimes({ name: "Pam" }, 5678)
// -> Hello Pam undefined! I've seen you 5678 times before.
sayHelloTimes(5678)
// -> Hello undefined undefined! I've seen you undefined times before.
```

假設參數被解構時不存在的話，會拋出例外，可能會造成你的應用程式停止：

```js
sayHelloTimes()
// -> Uncaught TypeError: Cannot match against 'undefined' or 'null'...
```

它的概念上類似於存取未定義對象的屬性，只是用不同的例外類型。

解構賦值某些程度上會隱藏所有預設參數：

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

`= {}` 掩蓋了 _object_ 屬性不存在的情況；但對於個別屬性預設值的情形下則是會拋出例外：

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

> 請注意解構賦值現在 Node.js 還有其他瀏覽器還無法使用。如果你想要試試看的話，你可以在 Node.js 使用 `--harmony-destructuring`。
