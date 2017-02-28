---
layout: post

title: Converting truthy/falsy values to boolean
tip-number: 30
tip-username: hakhag
tip-username-profile: https://github.com/hakhag
tip-tldr: Logical operators are a core part of JavaScript, here you can see a a way you always get a true or false no matter what was given to it.


redirect_from:
  - /en/converting-truthy-falsy-values-to-boolean/

categories:
    - en
    - javascript
---

You can convert a [truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) or [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) value to true boolean with the `!!` operator.

```js
!!"" // false
!!0 // false
!!null // false
!!undefined // false
!!NaN // false

!!"hello" // true
!!1 // true
!!{} // true
!![] // true
```

