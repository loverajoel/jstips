---
layout: post

title: 返回对象，使方法可以链式调用
tip-number: 20
tip-username: WakeskaterX
tip-username-profile: https://twitter.com/WakeStudio
tip-tldr: 在面向对象的Javascript中为对象建立一个方法时，返回当前对象可以让你在一条链上调用方法。

redirect_from:
  - /zh_cn/return-objects-to-enable-chaining-of-functions/

categories:
    - zh_CN
    - javascript
---

在面向对象的Javascript中为对象建立一个方法时，返回当前对象可以让你在一条链上调用方法。

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
