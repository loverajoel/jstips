---
layout: post

title: ES6中的伪强制参数
tip-number: 12
tip-username: Avraam Mavridis
tip-username-profile: https://github.com/AvraamMavridis
tip-tldr: 在许多编程语言中，方法的参数时默认强制需要的，开发人员需要明确定义一个可选的参数。

categories:
    - zh_CN
---

在许多编程语言中，方法的参数时默认强制需要的，开发人员需要明确定义一个可选的参数。在Javascript中任何参数都是可选的，但是我们可以利用[**es6参数默认值**](http://exploringjs.com/es6/ch_parameter-handling.html#sec_parameter-default-values)特性的优点来实现强制要求这种表现而不污染本身的函数体。

```javascript
const _err = function( message ){
  throw new Error( message );
}

const getSum = (a = _err('a is not defined'), b = _err('b is not defined')) => a + b

getSum( 10 ) // throws Error, b is not defined
getSum( undefined, 10 ) // throws Error, a is not defined
 ```



 `_err`方法会立即抛出一个错误。如果没有传递值给参数，默认值将会被使用, `_err`方法将被调用而错误也将被抛出。你可以从[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Default_parameters)看到更多关于**默认参数特性**的例子。 
