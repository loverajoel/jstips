---
layout: post

title: Even simpler way of using `indexOf` as a contains clause
tip-number: 15
tip-username: jhogoforbroke
tip-username-profile: https://twitter.com/jhogoforbroke
tip-tldr: JavaScript by default does not have a contains method. And for checking existence of a substring in a string or an item in an array you may do this.

redirect_from:
  - /en/even-simpler-way-of-using-indexof-as-a-contains-clause/

categories:
    - en
    - javascript
---

JavaScript by default does not have a contains method. And for checking existence of a substring in a string or an item in an array you may do this:

```javascript
var someText = 'javascript rules';
if (someText.indexOf('javascript') !== -1) {
}

// or
if (someText.indexOf('javascript') >= 0) {
}
```

But let's look at these [Expressjs](https://github.com/strongloop/express) code snippets.

[examples/mvc/lib/boot.js](https://github.com/strongloop/express/blob/2f8ac6726fa20ab5b4a05c112c886752868ac8ce/examples/mvc/lib/boot.js#L26)


```javascript
for (var key in obj) {
  // "reserved" exports
  if (~['name', 'prefix', 'engine', 'before'].indexOf(key)) continue;
```

[lib/utils.js](https://github.com/strongloop/express/blob/2f8ac6726fa20ab5b4a05c112c886752868ac8ce/lib/utils.js#L93)


```javascript
exports.normalizeType = function(type){
  return ~type.indexOf('/')
    ? acceptParams(type)
    : { value: mime.lookup(type), params: {} };
};
```

[examples/web-service/index.js](https://github.com/strongloop/express/blob/2f8ac6726fa20ab5b4a05c112c886752868ac8ce/examples/web-service/index.js#L35)


```javascript
// key is invalid
if (!~apiKeys.indexOf(key)) return next(error(401, 'invalid api key'));
```

The gotcha is the [bitwise operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators) **~**, "Bitwise operators perform their operations on binary representations, but they return standard JavaScript numerical values."

It transforms `-1` into `0`, and `0` evaluates to `false` in JavaScript:

```javascript
var someText = 'text';
!!~someText.indexOf('tex'); // someText contains "tex" - true
!~someText.indexOf('tex'); // someText NOT contains "tex" - false
~someText.indexOf('asd'); // someText doesn't contain "asd" - false
~someText.indexOf('ext'); // someText contains "ext" - true
```

### String.prototype.includes()

ES6 introduced the [includes() method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes) and you can use it to determine whether or not a string includes another string:

```javascript
'something'.includes('thing'); // true
```

With ECMAScript 2016 (ES7) it is even possible to use these techniques with Arrays:

```javascript
!!~[1, 2, 3].indexOf(1); // true
[1, 2, 3].includes(1); // true
```

**Unfortunately, it is only supported in Chrome, Firefox, Safari 9 or above and Edge; not IE11 or lower.**
**It's better used in controlled environments.**