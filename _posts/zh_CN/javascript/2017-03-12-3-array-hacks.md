---
layout: post

title: Array 的三个技巧
tip-number: 64
tip-username: hassanhelfi
tip-username-profile: https://twitter.com/hassanhelfi
tip-tldr: 在 JavaScript 中 数组（Array）随处可见，使用ECMAScript 6 中的新特性 扩展运算符 你可以做很多很棒事情。在这边文章中，我将为你介绍在编码中有用的3个技巧。


categories:
    - zh_CN
    - javascript
---

在 JavaScript 中 数组（Array）随处可见，使用ECMAScript 6 中的新特性 [扩展运算符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_operator) 你可以做很多很棒事情。在这边文章中，我将为你介绍在编码中有用的3个技巧。

### 1. 迭代一个空数组

JavaScript 中直接创建的数组是松散的，以至于会有很多坑。试着用数组的构造方法创建一个数组，你就会明白我的意思。

```javascript
> const arr = new Array(4);
[undefined, undefined, undefined, undefined]
```

你会发现，通过一个讼案的数组去循环调用一些转换是非常难得。

```javascript
> const arr = new Array(4);
> arr.map((elem, index) => index);
[undefined, undefined, undefined, undefined]
```

想要解决这个问题，你可以使用在创建新数组的时候使用 `Array.apply`。

```javascript
> const arr = Array.apply(null, new Array(4));
> arr.map((elem, index) => index);
[0, 1, 2, 3]
```

### 2. 给方法传一个空参数

如果你想调用一个方法，并不填其中的一个参数时，JavaScript 就会报错。

```javascript
> method('parameter1', , 'parameter3');
Uncaught SyntaxError: Unexpected token ,
```

一个人们常用的解决方法是传递 `null` 或 `undefined`.

```javascript
> method('parameter1', null, 'parameter3') // or
> method('parameter1', undefined, 'parameter3');
```

自从 JavaScript 把 `null` 当做一个 object 的时候， 我个人就不太喜欢使用它了。根据 ES6 中对扩展运算符的介绍，有一个更简洁的方法可以将空参数传递给一个方法。正如前文所提到的，数组是松散的，所以给它传空值是可以的，我们正式用到了这个优点。

```javascript
> method(...['parameter1', , 'parameter3']); // works!
```

### 数组去重

我一直不明白为什么数组不提供一个内置函数可以让我们方便的取到去重以后的值。扩展运算符帮到了我们，使用扩展运算符配合 `Set` Spread operators are here for the rescue. Use spread operators with the `Set` 可以生成一个不重复的数组。

```javascript
> const arr = [...new Set([1, 2, 3, 3])];
[1, 2, 3]
```
