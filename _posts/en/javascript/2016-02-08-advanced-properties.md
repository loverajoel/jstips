---
layout: post

title: Advanced Javascript Properties
tip-number: 39
tip-username: mallowigi
tip-username-profile: https://github.com/mallowigi
tip-tldr: How to add private properties, getters and setters to objects.


redirect_from:
  - /en/advanced-properties/

categories:
    - en
    - javascript
---

It is possible to configure object properties in Javascript for example to set properties to be pseudo-private or readonly. This feature is available since ECMAScript 5.1, therefore supported by all recent browsers.

To do so, you need to use the method `defineProperty` of the `Object` prototype like so:

```js
var a = {};
Object.defineProperty(a, 'readonly', {
  value: 15,
  writable: false
});

a.readonly = 20;
console.log(a.readonly); // 15
```

The syntax is as follows: 
```js
Object.defineProperty(dest, propName, options)
```

or for multiple definitions:
```js
Object.defineProperties(dest, {
  propA: optionsA,
  propB: optionsB, //...
})
```

where options include the following attributes:
- *value*: if the property is not a getter (see below), value is a mandatory attribute. `{a: 12}` === `Object.defineProperty(obj, 'a', {value: 12})`
- *writable*: set the property as readonly. Note that if the property is a nested objects, its properties are still editable.
- *enumerable*: set the property as hidden. That means that `for ... of` loops and `stringify` will not include the property in their result, but the property is still there. Note: That doesn't mean that the property is private! It can still be accessible from the outside, it just means that it won't be printed.
- *configurable*: set the property as non modifiable, e.g. protected from deletion or redefinition. Again, if the property is a nested object, its properties are still configurable.


So in order to create a private constant property, you can define it like so:

```js
Object.defineProperty(obj, 'myPrivateProp', {value: val, enumerable: false, writable: false, configurable: false});
```

Besides configuring properties, `defineProperty` allows us to define *dynamic properties*, thanks to the second parameter being a string. For instance, let's say that I want to create properties according to some external configuration:

```js

var obj = {
  getTypeFromExternal(): true // illegal in ES5.1
}

Object.defineProperty(obj, getTypeFromExternal(), {value: true}); // ok

// For the example sake, ES6 introduced a new syntax:
var obj = {
  [getTypeFromExternal()]: true
}
```

But that's not all! Advanced properties allows us to create **getters** and **setters**, just like other OOP languages! In that case, one cannot use the `writable`, `enumerable` and `configurable` properties, but instead:

```js
function Foobar () {
  var _foo; //  true private property

  Object.defineProperty(obj, 'foo', {
    get: function () { return _foo; }
    set: function (value) { _foo = value }
  });

}

var foobar = new Foobar();
foobar.foo; // 15
foobar.foo = 20; // _foo = 20
```

Aside for the obvious advantage of encapsulation and advanced accessors, you will notice that we didn't "call" the getter, instead we just "get" the property without parentheses! This is awesome! For instance, let's imagine that we have an object with long nested properties, like so:

```js
var obj = {a: {b: {c: [{d: 10}, {d: 20}] } } };
```

Now instead of doing `a.b.c[0].d` (where one of the properties can resolve to `undefined` and throw an error), we can instead create an alias:

```js
Object.defineProperty(obj, 'firstD', {
  get: function () { return a && a.b && a.b.c && a.b.c[0] && a.b.c[0].d }
})

console.log(obj.firstD) // 10
```

### Note
If you define a getter without a setter and still try to set a value, you will get an error! This is particularly important when using helper functions such as `$.extend` or `_.merge`. Be careful!

### Links

- [defineProperty](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)
- [Defining properties in JavaScript](http://bdadam.com/blog/defining-properties-in-javascript.html)
