---
layout: post

title: undefined与null的区别
tip-number: 05
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: 理解`undefined`与`null`的区别。
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /zh_cn/differences-between-undefined-and-null/

categories:
    - zh_CN
    - javascript
---


- `undefined`表示一个变量没有被声明，或者被声明了但没有被赋值
- `null`是一个表示“没有值”的值
- Javascript将未赋值的变量默认值设为`undefined`
- Javascript从来不会将变量设为`null`。它是用来让程序员表明某个用`var`声明的变量时没有值的。
- `undefined`不是一个有效的JSON，而`null`是
- `undefined`的类型(typeof)是`undefined`
- `null`的类型(typeof)是`object`. [为什么?](http://www.2ality.com/2013/10/typeof-null.html)
- 它们都是基本类型
- 他们都是[falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)
  (`Boolean(undefined) // false`, `Boolean(null) // false`)
- 你可以这样判断一个变量是否是[undefined](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined)

```javascript
  typeof variable === "undefined"
```

- 你可以这样判断一个变量是否是[null](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/null)

```javascript
  variable === null
```

- **双等号**比较时它们相等，但**三等号**比较时不相等

```javascript
  null == undefined // true

  null === undefined // false
```
