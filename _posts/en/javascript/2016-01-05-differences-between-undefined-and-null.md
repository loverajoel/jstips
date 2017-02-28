---
layout: post

title: Differences between `undefined` and `null`
tip-number: 05
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: Understanding the differences between `undefined` and `null`.
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /en/differences-between-undefined-and-null/

categories:
    - en
    - javascript
---

- `undefined` means a variable has not been declared, or has been declared but has not yet been assigned a value
- `null` is an assignment value that means "no value"
- Javascript sets unassigned variables with a default value of `undefined`
- Javascript never sets a value to `null`. It is used by programmers to indicate that a `var` has no value.
- `undefined` is not valid in JSON while `null` is
- `undefined` typeof is `undefined`
- `null` typeof is an `object`. [Why?](http://www.2ality.com/2013/10/typeof-null.html)
- Both are primitives
- Both are [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)
  (`Boolean(undefined) // false`, `Boolean(null) // false`)
- You can know if a variable is [undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)

  ```javascript
  typeof variable === "undefined"
```
- You can check if a variable is [null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null)

  ```javascript
  variable === null
```
- The **equality** operator considers them equal, but the **identity** doesn't

  ```javascript
  null == undefined // true

  null === undefined // false
```