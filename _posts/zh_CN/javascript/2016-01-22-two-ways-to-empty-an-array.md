---
layout: post

title: 清空数组的两种方法
tip-number: 22
tip-username: microlv
tip-username-profile: https://github.com/microlv
tip-tldr: 在JavaScript中清空一个数组有很多方法，但这是一个最高效的方法。

redirect_from:
  - /zh_cn/two-ways-to-empty-an-array/

categories:
    - zh_CN
    - javascript
---

如果你定义了一个数组，然后你想清空它。
通常，你会这样做：

```javascript
// 定义一个数组
var list = [1, 2, 3, 4];
function empty() {
    //清空数组
    list = [];
}
empty();
```

但是，这有一个效率更高的方法来清空数组。
你可以这样写:

```javascript
var list = [1, 2, 3, 4];
function empty() {
    //empty your array
    list.length = 0;
}
empty();
```

* `list = []` 将一个新的数组的引用赋值给变量，其他引用并不受影响。
这意味着以前数组的内容被引用的话将依旧存在于内存中，这将导致内存泄漏。

* `list.length = 0` 删除数组里的所有内容，也将影响到其他引用。

然而，如果你复制了一个数组（A 和 Copy-A），如果你用`list.length = 0`清空了它的内容，复制的数组也会清空它的内容。

考虑一下将会输出什么：

```js
var foo = [1,2,3];
var bar = [1,2,3];
var foo2 = foo;
var bar2 = bar;
foo = [];
bar.length = 0;
console.log(foo, bar, foo2, bar2);

//[] [] [1, 2, 3] []
```

更多内容请看Stackoverflow：
[difference-between-array-length-0-and-array](http://stackoverflow.com/questions/4804235/difference-between-array-length-0-and-array)

