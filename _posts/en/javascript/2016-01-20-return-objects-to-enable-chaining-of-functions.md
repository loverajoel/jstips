---
layout: post

title: Return objects to enable chaining of functions
tip-number: 20
tip-username: WakeskaterX
tip-username-profile: https://twitter.com/WakeStudio
tip-tldr: When creating functions on an object in Object Oriented Javascript, returning the object in the function will enable you to chain functions together.

redirect_from:
  - /en/return-objects-to-enable-chaining-of-functions/

categories:
    - en
    - javascript
---

When creating functions on an object in Object Oriented Javascript, returning the object in the function will enable you to chain functions together.

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