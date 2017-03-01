---
layout: post

title: Javascript高级特性
tip-number: 39
tip-username: mallowigi
tip-username-profile: https://github.com/mallowigi
tip-tldr: 怎样给一个对象添加私有参数、`getter`或`setter`。


redirect_from:
  - /zh_cn/advanced-properties/

categories:
    - zh_CN
    - javascript
---

在Javascript里配置对象属性是可以实现的，比如将一个参数设为伪私有或者只读。这个特性从ECMAScript 5.1开始就可以使用了，因此近来的浏览器都是支持的。
要实现这些功能，你需要使用`Object`的原型方法`defineProperty`，像这样：

```js
var a = {};
Object.defineProperty(a, 'readonly', {
  value: 15,
  writable: false
});

a.readonly = 20;
console.log(a.readonly); // 15
```

语法如下：

```js
Object.defineProperty(dest, propName, options);
```

或者定义多个：

```js
Object.defineProperties(dest, {
  propA: optionsA,
  propB: optionsB, //...
});
```

`options`包含如下的属性：
- *value*: 如果参数不是`getter`（请看下文），`value`是必须的。`{a: 12}` === `Object.defineProperty(obj, 'a', {value: 12})`
- *writable*: 将参数设为只读。需要注意的是如果参数是嵌套对象，它的元素仍是能可修改的。
- *enumerable*: 将参数设为隐藏。这意味着`for ... of`循环和`stringify`的结果里不会包含这些参数，但是这个参数还是存在的。提示：这并不意味着参数是私有的！他依旧可以从外界访问，只是意味着不会被打印。
- *configurable*: 将属性设置为不能更改，比如：防止参数被删除或重新定义。如果此对象是一个嵌套对象，他的参数依旧是可配置的。


所以如果想创建私有静态变量，你可以这样定义：

```js
Object.defineProperty(obj, 'myPrivateProp', {value: val, enumerable: false, writable: false, configurable: false});
```

除了配置属性，由于`defineProperty`第二个参数是字符串，所以允许我们定义*动态变量(defineProperty)*。例如，我们可以说我们要根据一些外部配置创建一个属性：

```js

var obj = {
  getTypeFromExternal(): true // illegal in ES5.1
};

Object.defineProperty(obj, getTypeFromExternal(), {value: true}); // ok

// For the example sake, ES6 introduced a new syntax:
var obj = {
  [getTypeFromExternal()]: true
};
```

还没有结束！高级特性允许我们创建**getter**和**setter**，就像其他面向对象(OOP)语言！这种情况下，我们不能使用`writable`、`enumerable`和`configurable`参数，而是：

```js
function Foobar () {
  var _foo; //  true private property

  Object.defineProperty(obj, 'foo', {
    get: function () { return _foo; }
    set: function (value) { _foo = value }
  });

};

var foobar = new Foobar();
foobar.foo; // 15
foobar.foo = 20; // _foo = 20
```

除了封装与先进的访问器这些明显的优点，你还发现我们并没有“调用”`getter`，而是不需要使用小括号直接“取得”了属性！这太棒了！例如，我们可以想象我们有一个多层嵌套对象，像这样：

```js
var obj = {a: {b: {c: [{d: 10}, {d: 20}] } } };
```

现在我们不需要调用`a.b.c[0].d`（其中某个属性可能是`undefined`且抛出错误），我们可以创建一个别名：

```js
Object.defineProperty(obj, 'firstD', {
  get: function () { return a && a.b && a.b.c && a.b.c[0] && a.b.c[0].d }
});

console.log(obj.firstD); // 10
```

### 提示

如果你定义了`getter`而没有定义`setter`却仍要给它赋值，你将会得到一个错误。这在使用像`$.extend`或`_.merge`这样的辅助方法时是尤为重要的。要小心！

### 链接

- [defineProperty](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)
- [Defining properties in JavaScript](http://bdadam.com/blog/defining-properties-in-javascript.html)
