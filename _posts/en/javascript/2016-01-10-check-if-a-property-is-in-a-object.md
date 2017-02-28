---
layout: post

title: Check if a property is in a Object
tip-number: 10
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: These are ways to check if a property is present in an object.
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /en/check-if-a-property-is-in-a-object/

categories:
    - en
    - javascript
---

When you have to check if a property is present in an [object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects), you probably are doing something like this:

```javascript
var myObject = {
  name: '@tips_js'
};

if (myObject.name) { ... }

```

That's ok, but you have to know that there are two native ways for this kind of thing, the [`in` operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in) and [`Object.hasOwnProperty`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty). Every object descended from `Object`, has both ways available.

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

Both differ in the depth at which they check the properties. In other words, `hasOwnProperty` will only return true if key is available on that object directly. However, the `in` operator doesn't discriminate between properties created on an object and properties inherited from the prototype chain.

Here's another example:

```javascript
var myFunc = function() {
  this.name = '@tips_js';
};
myFunc.prototype.age = '10 days';

var user = new myFunc();

user.hasOwnProperty('name'); // true
user.hasOwnProperty('age'); // false, because age is from the prototype chain
```

Check the [live examples here](https://jsbin.com/tecoqa/edit?js,console)!

I also recommend reading [this discussion](https://github.com/loverajoel/jstips/issues/62) about common mistakes made when checking a property's existence in objects.