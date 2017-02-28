---
layout: post

title: Use === instead of ==
tip-number: 24
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: The `==` (or `!=`) operator performs an automatic type conversion if needed. The `===` (or `!==`) operator will not perform any conversion. It compares the value and the type, which could be considered faster ([jsPref](http://jsperf.com/strictcompare)) than `==`.

redirect_from:
  - /en/use_===_instead_of_==/

categories:
    - en
    - javascript
---

The `==` (or `!=`) operator performs an automatic type conversion if needed. The `===` (or `!==`) operator will not perform any conversion. It compares the value and the type, which could be considered faster ([jsPref](http://jsperf.com/strictcompare)) than `==`.

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
