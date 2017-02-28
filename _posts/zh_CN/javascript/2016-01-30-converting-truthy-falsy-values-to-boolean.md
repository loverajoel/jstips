---
layout: post

title: 将truthy/falsy转换为布尔值
tip-number: 30
tip-username: hakhag
tip-username-profile: https://github.com/hakhag
tip-tldr: 逻辑运算符是JavaScript的核心之一，在这里你将看到一种无论你传什么值都可以总是得到true或false的方法。


redirect_from:
  - /zh_cn/converting-truthy-falsy-values-to-boolean/

categories:
    - zh_CN
    - javascript
---

你可以使用`!!`操作符将[truthy](https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy)或[falsy](https://developer.mozilla.org/zh-CN/docs/Glossary/Falsy)值转换为布尔值。

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

