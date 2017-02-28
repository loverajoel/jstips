---
layout: post

title: Converting to number fast way
tip-number: 23
tip-username: sonnyt
tip-username-profile: http://twitter.com/sonnyt
tip-tldr: Converting strings to numbers is extremely common. The easiest and fastest way to achieve that would be using the + operator.

redirect_from:
  - /en/converting-to-number-fast-way/

categories:
    - en
    - javascript
---

Converting strings to numbers is extremely common. The easiest and fastest ([jsPerf](https://jsperf.com/number-vs-parseint-vs-plus/29)) way to achieve that would be using the `+` (plus) operator.

```javascript
var one = '1';

var numberOne = +one; // Number 1
```

You can also use the `-` (minus) operator which type-converts the value into number but also negates it.

```javascript
var one = '1';

var negativeNumberOne = -one; // Number -1
```
