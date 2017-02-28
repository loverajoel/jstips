---
layout: post

title: Pseudomandatory parameters in ES6 functions
tip-number: 12
tip-username: Avraam Mavridis
tip-username-profile: https://github.com/AvraamMavridis
tip-tldr: In many programming languages the parameters of a function are by default mandatory and the developer has to explicitly define that a parameter is optional.

redirect_from:
  - /en/pseudomandatory-parameters-in-es6-functions/

categories:
    - en
    - javascript
---

In many programming languages the parameters of a function are by default mandatory and the developer has to explicitly define that a parameter is optional. In Javascript, every parameter is optional, but we can enforce this behavior without messing with the actual body of a function, taking advantage of [**es6's default values for parameters**] (http://exploringjs.com/es6/ch_parameter-handling.html#sec_parameter-default-values) feature.

```javascript
const _err = function( message ){
  throw new Error( message );
}

const getSum = (a = _err('a is not defined'), b = _err('b is not defined')) => a + b

getSum( 10 ) // throws Error, b is not defined
getSum( undefined, 10 ) // throws Error, a is not defined
```

 `_err` is a function that immediately throws an Error. If no value is passed for one of the parameters, the default value is going to be used, `_err` will be called and an Error will be thrown. You can see more examples for the **default parameters feature** on [Mozilla's Developer Network ](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/default_parameters)