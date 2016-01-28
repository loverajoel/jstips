---
layout: post

title: Remove duplicate primitive values from an Array
tip-number: 28
tip-username: danillouz
tip-username-profile: https://www.twitter.com/danillouz
tip-tldr: Remove duplicate primitive values from an Array.


categories:
    - en
---

You can deduplicate an Array by only using the `filter` and `indexOf` methods.

*Note that the following method only works when the elements of the
Array are primitive values.*

**ES5**
```javascript
var elems = [ 1, 1, 'a', 'a' ];

var dedup = elems.filter(function (el, i) {
	return elems.indexOf(el) === i;
});

console.log(dedup); // [ 1, 'a' ]
```

**ES2015**
```javascript
var elems = [ 1, 1, 'a', 'a' ];
var dedup = elems.filter( (el, i) => elems.indexOf(el) === i);

console.log(dedup); // [ 1, 'a' ]
```
