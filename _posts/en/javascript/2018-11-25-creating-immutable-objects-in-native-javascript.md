---
layout: post

title: Creating immutable objects in native JavaScript
tip-number: 74
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: With the latest versions of JavaScript it’s possible to create immutable objects. I’ll walk you through how to do it in three different ways.

categories:
    - en
    - javascript
---


# Creating immutable objects in native JavaScript
Javascript it’s a flexible language, you can redefine anything. But when projects get complex we find problems with mutable data structures.
With the latest versions of JavaScript this situation changed. Now it’s possible to create immutable objects. I’ll walk you through how to do it in three different ways.

### Wait, what means immutable?
> Immutability in object means we don’t want our objects to change in any ways once we create them i.e make them read-only type. 

Let’s suppose we need to define a car [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) and use its properties to perform operations throughout our entire project.
We can’t allow modifying by mistake any data.

```
const myTesla = {
	maxSpeed: 250,
	batteryLife: 300,
	weight: 123
};
```


## [Object.preventExtensions()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/preventExtensions)
This method prevents the addition of new properties to our existing object. 
`preventExtensions()` is a irreversible operation. We can never add extra properties to the object again.

```
Object.isExtensible(myTesla); // true
Object.preventExtensions(myTesla);
Object.isExtensible(myTesla); // false
myTesla.color = 'blue';
console.log(myTesla.color) // undefined
```

## [Object.seal()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/seal)
It prevents additions or deletion of properties. `seal()` also prevents the modification of property descriptors.

```
Object.isSealed(myTesla); // false
Object.seal(myTesla);
Object.isSealed(myTesla); // true

myTesla.color = 'blue';
console.log(myTesla.color); // undefined

delete myTesla.batteryLife; // false
console.log(myTesla.batteryLife); // 300

Object.defineProperty(myTesla, 'batteryLife'); // TypeError: Cannot redefine property: batteryLife
```

## [Object.freeze()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)
It does the same that `Object.seal()` plus it makes the properties non-writable.

```
Object.isFrozen(myTesla); // false
Object.freeze(myTesla);
Object.isFrozen(myTesla); // true

myTesla.color = 'blue';
console.log(myTesla.color); // undefined

delete myTesla.batteryLife;
console.log(myTesla.batteryLife); // 300

Object.defineProperty(myTesla, 'batteryLife'); // TypeError: Cannot redefine property: batteryLife

myTesla.batteryLife = 400;
console.log(myTesla.batteryLife); // 300
```

## Extra
Use `strict mode` if you want to throw an error when trying to modify an immutable object.
