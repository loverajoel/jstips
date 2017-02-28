---
layout: post

title: ES6中的伪强制参数
tip-number: 12
tip-username: Avraam Mavridis
tip-username-profile: https://github.com/AvraamMavridis
tip-tldr: 在许多编程语言中，方法的参数时默认强制需要的，开发人员需要明确定义一个可选的参数。

redirect_from:
  - /zh_cn/tip-to-measure-performance-of-a-javascript-block/

categories:
    - zh_CN
    - javascript
---

在许多编程语言中，方法的参数是默认强制需要的，开发人员必须明确定义一个可选的参数。在Javascript 中每一个参数都是可选的，但是我们可以利用[**es6参数默认值**](http://exploringjs.com/es6/ch_parameter-handling.html#sec_parameter-default-values)特性的优点来达到强制要求这种目的，并且不污染函数体本身。

``` javascript
const _err = function( message ){

  throw new Error( message );

}

const getSum = (a = _err('a is not defined'), b = _err('b is not defined')) => a + b

getSum( 10 ) // throws Error, b is not defined

getSum( undefined, 10 ) // throws Error, a is not defined
```

 `_err`  是一个即时抛出错误的方法。如果参数中的任何一个没有值，参数默认的值将会被使用， `_err`方法将被调用，并且会抛出一个错误。你可以从[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Default_parameters)看到更多关于**默认参数特性**的例子。 