---
layout: post

title: 使用 === 而不是 ==
tip-number: 24
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: == (或者 `!=`) 操作在需要的情况下自动进行了类型转换。`===` (或 `!==`)操作不会执行任何转换。`===`在比较值和类型时，可以说比`==`更快。

redirect_from:
  - /zh_cn/use_===_instead_of_==/

categories:
    - zh_CN
    - javascript
---

`==` (或者 `!=`) 操作在需要的情况下自动进行了类型转换。`===` (或 `!==`)操作不会执行任何转换。`===`在比较值和类型时，可以说比`==`更快([jsPref](http://jsperf.com/strictcompare))。 

```js
[10] ==  10      // 为 true
[10] === 10      // 为 false

'10' ==  10      // 为 true
'10' === 10      // 为 false

 []  ==  0       // 为 true
 []  === 0       // 为 false

 ''  ==  false   // 为 true 但 true == "a" 为false
 ''  === false   // 为 false 

```
