---
layout: post

title: Safe string concatenation
tip-number: 19
tip-username: gogainda
tip-username-profile: https://twitter.com/gogainda
tip-tldr: Suppose you have a couple of variables with unknown types and you want to concatenate them in a string. To be sure that the arithmetical operation is not be applied during concatenation, use concat

redirect_from:
  - /en/safe-string-concatenation/

categories:
    - en
    - javascript
---

Suppose you have a couple of variables with unknown types and you want to concatenate them in a string. To be sure that the arithmetical operation is not be applied during concatenation, use `concat`:

```javascript
var one = 1;
var two = 2;
var three = '3';

var result = ''.concat(one, two, three); //"123"
```

This way of concatenting does exactly what you'd expect. In contrast, concatenation with pluses might lead to unexpected results:

```javascript
var one = 1;
var two = 2;
var three = '3';

var result = one + two + three; //"33" instead of "123"
```

Speaking about performance, compared to the `join` [type](http://www.sitepoint.com/javascript-fast-string-concatenation/) of concatenation, the speed of `concat` is pretty much the same.

You can read more about the `concat` function on MDN [page](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/concat).