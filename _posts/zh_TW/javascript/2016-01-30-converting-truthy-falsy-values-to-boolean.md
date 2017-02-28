---
layout: post

title: 將 truthy 和 falsy 轉換成布林值
tip-number: 30
tip-username: hakhag
tip-username-profile: https://github.com/hakhag
tip-tldr: 邏輯運算子是 JavaScript 核心之一 ，在這裡你可以發現這個方式，不管你給他什麼值，都會得到 true 或 false 。


redirect_from:
  - /zh_tw/converting-truthy-falsy-values-to-boolean/

categories:
    - zh_TW
    - javascript
---

你可以使用 `!!` 運算子將 [truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) 或 [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) 轉換成布林值。

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
