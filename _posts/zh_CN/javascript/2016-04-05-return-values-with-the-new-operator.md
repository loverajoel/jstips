---
layout: post

title: new的返回值
tip-number: 52
tip-username: Morklympious
tip-username-profile: https://github.com/morklympious
tip-tldr: 理解使用new与不使用new时将返回什么值

redirect_from:
  - /zh_cn/return-values-with-the-new-operator/

categories:
    - zh_CN
    - javascript
---

你将会遇到在JavaScript中使用`new`来分配新对象的一些情况。这将会扰乱你的思绪，除非你阅读了这篇文章并理解在内部发生了什么。

JavaScript中的`new`操作在合理的情况下然会一个新的对象实例。我们来看，我们有一个构造函数：

````js
function Thing() {
  this.one = 1;
  this.two = 2;
}

var myThing = new Thing();

myThing.one // 1
myThing.two // 2
````

__提示__: `this`指向`new`产生的新对象。否则如果`Thing()`不是用`new`调用, __将不会生成新对象__, 而且`this` 将会指向全局对象，也就是`window`。这意味着：

1. 你突然有两个全局变量`one`和`two`。
2. `myThing`现在为`undefined`，因为`Thing()`中没有返回任何东西。

现在我们又有一个例子，而它却有些让人搞不懂。我们看我在构造函数里加了一条语句：

````js
function Thing() {
  this.one = 1;
  this.two = 2;

  return 5;
}

var myThing = new Thing();
````

现在`myThing`等于什么呢？5？一个对象？还是我受伤的自我价值观？或许永远不知道！

除了能知道：

````js
myThing.one // 1
myThing.two // 2
````

很有趣，我们构造函数里`返回`的5怎么找不到了？这很奇怪不是吗？函数都做了什么？5呢？让我们再试试别的。

我们返回一个非原始类型试一下，比如一个对象：

````js
function Thing() {
  this.one = 1;
  this.two = 2;

  return {
    three: 3,
    four: 4
  };
}

var myThing = new Thing();
````

让我们试一试。直接`console.log`出所有内容：

````js
console.log(myThing);
/*
  Object {three: 3, four: 4}
  this.one 和 this.two发生了什么!?
  他们被覆盖了，朋友。
*/
````

__我们了解到：__ 当你使用`new`关键字调用一个函数的时候，你可以使用`this`关键字给其设置参数（但这些你应该已经知道了）。使用`new`关键字调用一个返回原始变量的函数将不会返回你指定的值，而是返回函数的实例`this`（你指定参数的那个对象，像 `this.one = 1;`).

然而，返回一个非原始变量像`object`、`array`或`function`将会覆盖`this`实例，并返回那个非原始变量，有效的破坏了你分配给`this`的所有工作。
