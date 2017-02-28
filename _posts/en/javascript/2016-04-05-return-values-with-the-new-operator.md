---
layout: post

title: Return Values with the 'new' Operator
tip-number: 52
tip-username: Morklympious
tip-username-profile: https://github.com/morklympious
tip-tldr: Understand what gets returned when using new vs. not using new.

redirect_from:
  - /en/return-values-with-the-new-operator/

categories:
    - en
    - javascript
---

You're going to run into some instances where you'll be using `new` to allocate new objects in JavaScript. It's going to blow your mind unless you read this tip to understand what's happening behind the scenes.

The `new` operator in JavaScript is an operator that, under reasonable circumstances, returns a new instance of an object. Let's say we have a constructor function:

````js
function Thing() {
  this.one = 1;
  this.two = 2;
}

var myThing = new Thing();

myThing.one // 1
myThing.two // 2
````

__Note__: `this` refers to the new object created by `new`. Otherwise if `Thing()` is called without `new`, __no object is created__, and `this` is going to point to the global object, which is `window`. This means that:

1. You'll suddenly have two new global variables named `one` and `two`.
2. `myThing` is now undefined, since nothing is returned in `Thing()`.

Now that you get that example, here's where things get a little bit wonky. Let's say I add something to the constructor function, a little SPICE:

````js
function Thing() {
  this.one = 1;
  this.two = 2;

  return 5;
}

var myThing = new Thing();
````

Now, what does myThing equal? Is it 5? is it an object? Is it my crippled sense of self-worth? The world may never know!

Except the world does know:

````js
myThing.one // 1
myThing.two // 2
````

Interestingly enough, we never actually see the five that we supposedly 'returned' from our constructor. That's weird, isn't it? What are you doing function? WHERE'S THE FIVE? Let's try it with something else.

Let's return a non-primitive type instead, something like an object.

````js
function Thing() {
  this.one = 1;
  this.two = 2;

  return {
    three: 3,
    four: 4
  };
}

var myThing = new Thing();
````

Let's check it out. A quick console.log reveals all:

````js
console.log(myThing);
/*
  Object {three: 3, four: 4}
  What happened to this.one and this.two!?
  They've been stomped, my friend.
*/
````

__Here's where we learn:__ When you invoke a function with the `new` keyword, you can set properties on it using the keyword `this` (but you probably already knew that). Returning a primitive value from a function you called with the `new` keyword will not return the value you specified, but instead will return the `this` instance of the function (the one you put properties on, like `this.one = 1;`).

However, returning a non-primitive, like an `object`, `array`, or `function` will stomp on the `this` instance, and return that non-primitive instead, effectively ruining all the hard work you did assigning everything to `this`.
