---
layout: post

title: 使用 === 來替代 ==
tip-number: 24
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: ==（或 !=）運算子如果在執行上需要的話，會自動將類型轉換。 `===`（或 `!==`）運算子則不會執行轉換。`===`（或 `!==`）用來比較數值和類型，相較於 `==` 更來的快速。

redirect_from:
  - /zh_tw/use_===_instead_of_==/

categories:
    - zh_TW
    - javascript
---

`==`（或 `!=`）運算子如果在執行上需要的話，會自動將類型轉換。 `===`（或 `!==`）運算子則不會執行轉換。`===`（或 `!==`）用來比較數值和類型，相較於 `==` 更來的快速。（[jsPref](http://jsperf.com/strictcompare)）

```js
[10] ==  10      // is true
[10] === 10      // is false

'10' ==  10      // is true
'10' === 10      // is false

 []  ==  0       // is true
 []  === 0       // is false

 ''  ==  false   // is true but true == "a" is false
 ''  === false   // is false

```
