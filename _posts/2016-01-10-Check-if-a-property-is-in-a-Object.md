---
layout: default
title: "Check if a property is in a Object"
author: "@loverajoel"
author-link: https://www.twitter.com/loverajoel
---

When you have to check if a property is present of an [object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects), you probably are doing something like this:

```javascript
var myObject = {
  name: '@tips_js'
};

if (myObject.name) { ... }

```

Thats ok, but you have to know that there are two native ways for this kind of thing, the [`in` operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in) and [`Object.hasOwnProperty`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty), every object descended from `Object`, has available both ways.

### See the big Difference

```javascript
var myObject = {
  name: '@tips_js'
};

myObject.hasOwnProperty('name'); // true
'name' in myObject; // true

myObject.hasOwnProperty('valueOf'); // false, valueOf is inherited from the prototype chain
'valueOf' in myObject; // true

```

Both differs in the depth how check the properties, in other words `hasOwnProperty` will only return true if key is available on that object directly, however `in` operator doesn't discriminate between properties created on an object and properties inherited from the prototype chain.

Here another example

```javascript
var myFunc = function() {
  this.name = '@tips_js';
};
myFunc.prototype.age = '10 days';

var user = new myFunc();

user.hasOwnProperty('name'); // true
user.hasOwnProperty('age'); // false, because age is from the prototype chain
```

Check here the [live examples](https://jsbin.com/tecoqa/edit?js,console)!

Also recommends read [this discussion](https://github.com/loverajoel/jstips/issues/62) about common mistakes at checking properties' existence in objects
