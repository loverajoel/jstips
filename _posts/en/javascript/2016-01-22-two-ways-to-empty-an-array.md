---
layout: post

title: Two ways to empty an array
tip-number: 22
tip-username: microlv
tip-username-profile: https://github.com/microlv
tip-tldr: In JavaScript when you want to empty an array, there are a lot ways, but this is the most performant.

redirect_from:
  - /en/two-ways-to-empty-an-array/

categories:
    - en
    - javascript
---

You define an array and want to empty its contents.
Usually, you would do it like this:

```javascript
// define Array
var list = [1, 2, 3, 4];
function empty() {
    //empty your array
    list = [];
}
empty();
```
But there is another way to empty an array that is more performant.

You should use code like this:

```javascript
var list = [1, 2, 3, 4];
function empty() {
    //empty your array
    list.length = 0;
}
empty();
```

* `list = []` assigns a reference to a new array to a variable, while any other references are unaffected.
which means that references to the contents of the previous array are still kept in memory, leading to memory leaks.

* `list.length = 0` deletes everything in the array, which does hit other references.

In other words, if you have two references to the same array (`a = [1,2,3]; a2 = a;`), and you delete the array's contents using `list.length = 0`, both references (a and a2) will now point to the same empty array. (So don't use this technique if you don't want a2 to hold an empty array!)

Think about what this will output:

```js
var foo = [1,2,3];
var bar = [1,2,3];
var foo2 = foo;
var bar2 = bar;
foo = [];
bar.length = 0;
console.log(foo, bar, foo2, bar2);

// [] [] [1, 2, 3] []
```

Stackoverflow more detail:
[difference-between-array-length-0-and-array](http://stackoverflow.com/questions/4804235/difference-between-array-length-0-and-array)
