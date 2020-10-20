---
layout: post

title: What is Functional Inheritance?
tip-number: 75
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: Functional inheritance is the process of inheriting features by applying an augmenting function to an object instance.

categories:
    - en
    - javascript
---

Functional inheritance is the process of inheriting features by applying an augmenting function to an object instance. The function supplies a closure scope which you can use to keep some data private. The augmenting function uses dynamic object extension to extend the object instance with new properties and methods.

Functional mixins are composable factory functions that add properties and behaviors to objects like stations in an assembly line.

```javascript
// Base object constructor function
function Animal(data) {
  var that = {}; // Create an empty object
  that.name = data.name; // Add it a "name" property
  return that; // Return the object
};

// Create achild object, inheriting from the base Animal
function Cat(data) {
  // Create the Animal object
  var that = Animal(data);
  // Extend base object
  that.sayHello = function() {
    return 'Hello, I\'m ' + that.name;
  };
  return that;
};

// Usage
var myCat = Cat({ name: 'Rufi' });
console.log(myCat.sayHello());
// Output: "Hello, I'm Rufi"
```


