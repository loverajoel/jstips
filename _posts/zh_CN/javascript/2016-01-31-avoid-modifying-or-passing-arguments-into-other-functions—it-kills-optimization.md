---
layout: post

title: 避免修改和传递`arguments`给其他方法 — 影响优化
tip-number: 31
tip-username: berkana
tip-username-profile: https://github.com/berkana
tip-tldr: 在JavaScript的方法里，`arguments`参数可以让你访问传递给该方法的所有参数。`arguments`是一个*类数组对象*；`arguments`可是使用数组标记访问，而且它有*length*参数，但是它没有`filter`、`map`和`forEach`这样内建到数组内的方法。因此，如下代码是一个非常常见的将`arguments`转换为数组的办法


redirect_from:
  - /zh_cn/avoid-modifying-or-passing-arguments-into-other-functions-it-kills-optimization/

categories:
    - zh_CN
    - javascript
---

### 背景

在JavaScript的方法里，[`arguments`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/arguments)参数可以让你访问传递给该方法的所有参数。`arguments`是一个*类数组对象*；`arguments`可是使用数组标记访问，而且它有*length*参数，但是它没有`filter`、`map`和`forEach`这样内建到数组内的方法。因此，如下代码是一个非常常见的将`arguments`转换为数组的办法：

```js
var args = Array.prototype.slice.call(arguments);
```

将`arguments`传递给`Array`原型(prototype)上的`slice`方法；`slice`方法返回一个对`arguments`浅复制后的数组对象。更短的写法：

```js
var args = [].slice.call(arguments);
```

在这里，简单的调用了空数组的`slice`方法，而没有从`Array`的原型(prototype)上调用。

### 系统优化

不幸的是，传递`arguments`给任何参数，将导致Chrome和Node中使用的V8引擎跳过对其的优化，这也将使性能相当慢。看一下这篇文章[optimization killers](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers)。传递`arguments`给任何方法被称为*leaking `arguments`*。

如果你想用一个包含参数(arguments)的数组，你需要求助于这个办法：

```js
var args = new Array(arguments.length);
for(var i = 0; i < args.length; ++i) {
  args[i] = arguments[i];
}
```

没错，这很啰嗦，但是在生产环境中的代码里，为了系统性能优化，这是值得的。