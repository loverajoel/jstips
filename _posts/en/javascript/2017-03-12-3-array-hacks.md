---
layout: post

title: 3 Array Hacks
tip-number: 64
tip-username: hassanhelfi
tip-username-profile: https://twitter.com/hassanhelfi
tip-tldr: Arrays are everywhere and with the new spread operators introduced in ECMAScript 6, you can do awesome things with them. In this post I will show you 3 useful tricks you can use when programming.


categories:
    - en
    - javascript
---

Arrays are everywhere in JavaScript and with the new [spread operators](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Spread_operator) introduced in ECMAScript 6, you can do awesome things with them. In this post I will show you 3 useful tricks you can use when programming.

### 1. Iterating through an empty array

JavaScript arrays are sparse in nature in that there are a lot of holes in them. Try creating an array using the Array’s constructor and you will see what I mean.

```javascript
> const arr = new Array(4);
[undefined, undefined, undefined, undefined]
```

You may find that iterating over a sparse array to apply a certain transformation is hard.

```javascript
> const arr = new Array(4);
> arr.map((elem, index) => index);
[undefined, undefined, undefined, undefined]
```

To solve this, you can use `Array.apply` when creating the array.

```javascript
> const arr = Array.apply(null, new Array(4));
> arr.map((elem, index) => index);
[0, 1, 2, 3]
```

### 2. Passing an empty parameter to a method

If you want to call a method and ignore one of its parameters, then JavaScript will complain if you keep it empty.

```javascript
> method('parameter1', , 'parameter3');
Uncaught SyntaxError: Unexpected token ,
```

A workaround that people usually resort to is to pass either `null` or `undefined`.

```javascript
> method('parameter1', null, 'parameter3') // or
> method('parameter1', undefined, 'parameter3');
```

I personally don’t like using `null` since JavaScript treats it as an object and that’s just weird. With the introduction of spread operators in ES6, there is a neater way of passing empty parameters to a method. As previously mentioned, arrays are sparse in nature and so passing empty values to it is totally okay. We'll use this to our advantage.

```javascript
> method(...['parameter1', , 'parameter3']); // works!
```

### 3. Unique array values

I always wonder why the Array constructor does not have a designated method to facilitate the use of unique array values. Spread operators are here for the rescue. Use spread operators with the `Set` constructor to generate unique array values.

```javascript
> const arr = [...new Set([1, 2, 3, 3])];
[1, 2, 3]
```
