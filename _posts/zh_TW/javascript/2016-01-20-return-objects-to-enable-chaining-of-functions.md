---
layout: post

title: 回傳物件並使用函式鏈結
tip-number: 20
tip-username: WakeskaterX
tip-username-profile: https://twitter.com/WakeStudio
tip-tldr: 在 JavaScript 物件導向中，我們在物件上建立函式，函式回傳的物件讓你可以將函式鏈結在一起。

redirect_from:
  - /zh_tw/return-objects-to-enable-chaining-of-functions/

categories:
    - zh_TW
    - javascript
---

在 JavaScript 物件導向中，我們在物件上建立函式，函式回傳的物件讓你可以將函式鏈結在一起。

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
