---
layout: post

title: 转换为数字的更快方法
tip-number: 23
tip-username: sonnyt
tip-username-profile: http://twitter.com/sonnyt
tip-tldr: 将字符串转换为数字是极为常见的。最简单和快速的方法是使用`+`(加号) 来实现。

redirect_from:
  - /zh_cn/converting-to-number-fast-way/

categories:
    - zh_CN
    - javascript
---

将字符串转换为数字是极为常见的。最简单和快速的方法([jsPref](https://jsperf.com/number-vs-parseint-vs-plus/29))`+`(加号) 来实现。

```javascript
var one = '1';

var numberOne = +one; // Number 1
```

你也可以用`-`(减号)将其转化为负数值。

```javascript
var one = '1';

var negativeNumberOne = -one; // Number -1
```
