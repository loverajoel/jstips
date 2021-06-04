---
layout: post

titolo: Restituire oggetti per permettere il concatenamento di funzioni
tip-numero: 20
tip-username: WakeskaterX
tip-username-profile: https://twitter.com/WakeStudio
tip-tldr: Quando creiamo una funzione all'interno di un oggetto in Javascript Orientato agli Oggetti, restituire l'oggetto nella funzione vi permette di concatenare insieme le funzioni.

categoria:
    - it
---

Quando creiamo una funzione all'interno di un oggetto in Javascript Orientato agli Oggetti, restituire l'oggetto nella funzione vi permette di concatenare insieme le funzioni.

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
