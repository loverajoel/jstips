---
layout: post

title: Insert item inside an Array
tip-number: 00
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: Inserting an item into an existing array is a daily common task. You can add elements to the end of an array using push, to the beginning using unshift, or to the middle using splice.


categories:
    - en
---

Inserting an item into an existing array is a daily common task. You can add elements to the end of an array using push, to the beginning using unshift, or to the middle using splice.

Those are known methods, but it doesn't mean there isn't a more performant way. Here we go:

Adding an element at the end of the array is easy with push(), but there is a more performant way.

```javascript
var arr = [1,2,3,4,5];

arr.push(6);
arr[arr.length] = 6; // 43% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
Both methods modify the original array. Don't believe me? Check the [jsperf](http://jsperf.com/push-item-inside-an-array)

Now if we are trying to add an item to the beginning of the array:

```javascript
var arr = [1,2,3,4,5];

arr.unshift(0);
[0].concat(arr); // 98% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
Here is a little more detail: unshift edits the original array; concat returns a new array. [jsperf](http://jsperf.com/unshift-item-inside-an-array)

Adding items in the middle of an array is easy with splice, and it's the most performant way to do it.

```javascript
var items = ['one', 'two', 'three', 'four'];
items.splice(items.length / 2, 0, 'hello');
```

I tried to run these tests in various Browsers and OS and the results were similar. I hope these tips will be useful for you and encourage to perform your own tests!