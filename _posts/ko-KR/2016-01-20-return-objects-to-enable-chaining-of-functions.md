---
layout: post

title: 함수의 연속을 위해 객체를 반환하라
tip-number: 20
tip-username: WakeskaterX
tip-username-profile: https://twitter.com/WakeStudio
tip-tldr: OOP 자바스크립트에서 객체에 대한 함수를 만들때 객체를 반환해서 함수의 연속을 만들 수 있다.

categories:
    - ko
---
<translator: https://github.com/tisohjung>

OOP 자바스크립트에서 객체에 대한 함수를 만들때 객체를 반환해서 함수의 연속을 만들 수 있다.

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