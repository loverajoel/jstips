---
layout: default
title: "Pseudomentatory parameters in ES6 functions #ES6"
author: "Avraam Mavridis"
author-link: https://github.com/AvraamMavridis
---

In many programming languages the parameters of a function is by default mandatory and the developer has to explicitly define that a parameter is optional. In Javascript every parameter is optional, but we can enforce this behavior without messing the actual body of a function taking advantage of the [**es6's default values for parameters**] (http://exploringjs.com/es6/ch_parameter-handling.html#sec_parameter-default-values) feature.

```javascript
const _err = function( message ){
  throw new Error( message );
}

const getSum = (a = _err('a is not defined'), b = _err('b is not defined')) => a + b

getSum( 10 ) // throws Error, b is not defined
getSum( undefined, 10 ) // throws Error, a is not defined
 ```

 `_err` is a function that immediately throws an Error. If no value is passed for one of the parameters, the default value is gonna be used, `_err` will be called and an Error will be throwed. You can see more examples for the **default parameters feature** on [Mozilla's Developer Network ](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/default_parameters)
