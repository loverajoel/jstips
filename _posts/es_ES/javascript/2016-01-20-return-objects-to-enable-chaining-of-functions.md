---
layout: post

title: Devolver los objetos que permiten el encadenamiento de las funciones
tip-number: 20
tip-username: WakeskaterX
tip-username-profile: https://twitter.com/WakeStudio
tip-tldr: Al crear funciones en un objeto en Javascript orientado a objetos, devolver el objeto a la función le permitirá encadenar funciones.

redirect_from:
  - /es_es/return-objects-to-enable-chaining-of-functions/

categories:
    - es_ES
    - javascript
---

Al crear funciones en un objeto en Javascript orientado a objetos, devolver el objeto a la función le permitirá encadenar funciones.

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