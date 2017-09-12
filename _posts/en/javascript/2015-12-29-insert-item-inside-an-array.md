---
layout: post

title: Insert item inside an Array

tip-number: 00
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: Inserting an item into an existing array is a daily common task. You can add elements to the end of an array using push, to the beginning using unshift, or to the middle using splice.
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /en/insert-item-inside-an-array/

categories:
    - en
    - javascript
---

# Inserting an item into an existing array

Inserting an item into an existing array is a daily common task. You can add elements to the end of an array using push, to the beginning using unshift, or to the middle using splice.

Those are known methods, but it doesn't mean there isn't a more performant way. Here we go:

## Adding an element at the end

Adding an element at the end of the array is easy with push(), but it can be done in different ways.

```javascript

var arr = [1,2,3,4,5];
var arr2 = [];

arr.push(6);
arr[arr.length] = 6;
arr2 = arr.concat([6]);
```
Both first methods modify the original array. Don't believe me? Check the [jsperf](http://jsperf.com/push-item-inside-an-array)

### Performance on mobile :

#### Android (v4.2.2)

1. _arr.push(6);_ and _arr[arr.length] = 6;_ have the same performance // 3 319 694 ops/sec
3. _arr2 = arr.concat([6]);_ 50.61 % slower than the other two methods

#### Chrome Mobile (v33.0.0)

1. _arr[arr.length] = 6;_ // 6 125 975 ops/sec
2. _arr.push(6);_ 66.74 % slower
3. _arr2 = arr.concat([6]);_ 87.63 % slower

#### Safari Mobile (v9)

1. _arr[arr.length] = 6;_ // 7 452 898 ops/sec
2. _arr.push(6);_ 40.19 % slower
3. _arr2 = arr.concat([6]);_ 49.78 % slower

```javascript
Final victor

1. arr[arr.length] = 6; // with an average of 5 632 856 ops/sec
2. arr.push(6); // 35.64 % slower
3. arr2 = arr.concat([6]); // 62.67 % slower
```

### Performance on desktop

#### Chrome (v48.0.2564)

1. _arr[arr.length] = 6;_ // 21 602 722 ops/sec
2. _arr.push(6);_ 61.94 % slower
3. _arr2 = arr.concat([6]);_ 87.45 % slower

#### Firefox (v44)

1. _arr.push(6);_ // 56 032 805 ops/sec
2. _arr[arr.length] = 6;_ 0.52 % slower
3. _arr2 = arr.concat([6]);_ 87.36 % slower

#### IE (v11)

1. _arr[arr.length] = 6;_ // 67 197 046 ops/sec
2. _arr.push(6);_ 39.61 % slower
3. _arr2 = arr.concat([6]);_ 93.41 % slower

#### Opera (v35.0.2066.68)

1. _arr[arr.length] = 6;_ // 30 775 071 ops/sec
2. _arr.push(6);_ 71.60 % slower
3. _arr2 = arr.concat([6]);_ 83.70 % slower

#### Safari (v9.0.3)

1. _arr.push(6);_ // 42 670 978 ops/sec
2. _arr[arr.length] = 6;_ 0.80 % slower
3. _arr2 = arr.concat([6]);_ 76.07 % slower

```javascript
Final victor

1. arr[arr.length] = 6; // with an average of 42 345 449 ops/sec
2. arr.push(6); // 34.66 % slower
3. arr2 = arr.concat([6]); // 85.79 % slower
```

## Add an element at the beginning

Now if we are trying to add an item to the beginning of the array:

```javascript
var arr = [1,2,3,4,5];

arr.unshift(0);
[0].concat(arr);
```
Here is a little more detail: unshift edits the original array; concat returns a new array. [jsperf](http://jsperf.com/unshift-item-inside-an-array)

### Performance on mobile :

#### Android (v4.2.2)

1. _[0].concat(arr);_ // 1 808 717 ops/sec
2. _arr.unshift(0);_ 97.85 % slower

#### Chrome Mobile (v33.0.0)

1. _[0].concat(arr);_ // 1 269 498 ops/sec
2. _arr.unshift(0);_ 99.86 % slower

#### Safari Mobile (v9)

1. _arr.unshift(0);_ // 3 250 184 ops/sec
2. _[0].concat(arr);_ 33.67 % slower

```javascript
Final victor

1. [0].concat(arr); // with an average of 4 972 622 ops/sec
2. arr.unshift(0); // 64.70 % slower
```

### Performance on desktop

#### Chrome (v48.0.2564)

1. _[0].concat(arr);_ // 2 656 685 ops/sec
2. _arr.unshift(0);_ 96.77 % slower

#### Firefox (v44)

1. _[0].concat(arr);_ // 8 039 759 ops/sec
2. _arr.unshift(0);_ 99.72 % slower

#### IE (v11)

1. _[0].concat(arr);_ // 3 604 226 ops/sec
2. _arr.unshift(0);_ 98.31 % slower

#### Opera (v35.0.2066.68)

1. _[0].concat(arr);_ // 4 102 128 ops/sec
2. _arr.unshift(0);_ 97.44 % slower

#### Safari (v9.0.3)

1. _arr.unshift(0);_ // 12 356 477 ops/sec
2. _[0].concat(arr);_ 15.17 % slower

```javascript
Final victor

1. [0].concat(arr); // with an average of 6 032 573 ops/sec
2. arr.unshift(0); // 78.65 % slower
```

## Add an element in the middle

Adding items in the middle of an array is easy with splice, and it's the most performant way to do it.

```javascript
var items = ['one', 'two', 'three', 'four'];
items.splice(items.length / 2, 0, 'hello');
```

I tried to run these tests in various Browsers and OS and the results were similar. I hope these tips will be useful for you and encourage to perform your own tests!
