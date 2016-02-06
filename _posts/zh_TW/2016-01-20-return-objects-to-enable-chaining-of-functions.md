---
layout: post

title: Return objects to enable chaining of functions回傳物件並使用函式鏈結
tip-number: 20
tip-username: WakeskaterX
tip-username-profile: https://twitter.com/WakeStudio
tip-tldr: 在 JavaScript 物件導向中，當函數回傳的物件中，讓你可以將函式鏈結在一起。

categories:
    - zh_TW
---

在 JavaScript 物件導向中，當函數回傳的物件中，讓你可以將函式鏈結在一起。

```js
function Person(name) {
  this.name = name;

  this.sayName = function() {
    console.log("Hello my name is: ", this.name);
    return this;
  };

  this.changeName = function(name) {
    this.name = name;
    return this;
  };
}

var person = new Person("John");
person.sayName().changeName("Timmy").sayName();
```
