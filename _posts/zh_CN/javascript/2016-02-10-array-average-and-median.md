---
layout: post

title: 数组平均值与中值
tip-number: 41
tip-username: soyuka
tip-username-profile: https://github.com/soyuka
tip-tldr: 计算数组的平均值与中位数


redirect_from:
  - /zh_cn/array-average-and-median/

categories:
    - zh_CN
    - javascript
---

下面的例子都基于如下数组：

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
```

要取得平均值，我们需要将数字求和，然后除以`values`的数目，步骤如下：
- 取得数组长度(length)
- 求和(sum)
- 取得平均值(`sum/length`)

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
let sum = values.reduce((previous, current) => current += previous);
let avg = sum / values.length;
// avg = 28
```

或者：

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
let count = values.length;
values = values.reduce((previous, current) => current += previous);
values /= count;
// avg = 28
```

取得中值的步骤是：
- 将数组排序
- 取得中位数

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
values.sort((a, b) => a - b);
let lowMiddle = Math.floor((values.length - 1) / 2);
let highMiddle = Math.ceil((values.length - 1) / 2);
let median = (values[lowMiddle] + values[highMiddle]) / 2;
// median = 13,5
```

或者使用[无符号右移](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Right_shift)操作符：

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
values.sort((a, b) => a - b);
let median = (values[(values.length - 1) >> 1] + values[values.length >> 1]) / 2
// median = 23
```
