---
layout: post

title: 轉換為數字更快的方式
tip-number: 23
tip-username: sonnyt
tip-username-profile: http://twitter.com/sonnyt
tip-tldr: 轉換字串為數字是相當常見的。最簡單和快速的方式是使用 + 運算子來實現。

redirect_from:
  - /zh_tw/converting-to-number-fast-way/

categories:
    - zh_TW
    - javascript
---

轉換字串為數字是相當常見的。最簡單和快速的方式是使用 `+` （加號）運算子來實現。（[jsPerf](https://jsperf.com/number-vs-parseint-vs-plus/29)）

```javascript
var one = '1';

var numberOne = +one; // Number 1
```

你也可以使用 `-` （減號）運算子將數字類型轉換成負數。

```javascript
var one = '1';

var negativeNumberOne = -one; // Number -1
```
