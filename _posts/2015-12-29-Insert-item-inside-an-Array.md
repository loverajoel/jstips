---
layout: default
title: "Insert item inside an Array"
---

Inserting an item into an existing array is a daily common task. You can add elements to the end of an array using push, to the beginning using unshift, or the middle using splice.

But those are known methods, doesn't mean there isn't a more performant way, here we go...

Adding an element at the end of the array is easy with push(), but there is a way more performant.

```javascript
var arr = [1,2,3,4,5];

arr.push(6);
arr[arr.length] = 6; // 43% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
Both methods modify the original array. Don't believe me? Check the [jsperf](http://jsperf.com/push-item-inside-an-array)

Now we are trying to add an item to the beginning of the array

```javascript
var arr = [1,2,3,4,5];

arr.unshift(0);
[0].concat(arr); // 98% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
Here is a little bit detail, unshift edits the original array, concat returns a new array. [jsperf](http://jsperf.com/unshift-item-inside-an-array)

Adding items at the middle of an array is easy with splice and is the most performant way to do it.

```javascript
var items = ['one', 'two', 'three', 'four'];
items.splice(items.length / 2, 0, 'hello');
```

I tried to run these tests in various Browsers and OS and the results were similar. I hope these tips will be useful for you and encourage to perform your own tests!
