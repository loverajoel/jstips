---
layout: post

title: 陣列平均值和中間值
tip-number: 41
tip-username: soyuka
tip-username-profile: https://github.com/soyuka
tip-tldr: 計算陣列的平均值和中間值。


redirect_from:
  - /zh_tw/array-average-and-median/

categories:
    - zh_TW
    - javascript
---

以下範例基於一個陣列：

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
```

如果要取得平均，我們必須加總所有數字和再除以數字的個數。步驟是：
- 取得陣列長度
- 加總數值
- 取得平均（`數值總和 / 陣列長度`）

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
let sum = values.reduce((previous, current) => current += previous);
let avg = sum / values.length;
// avg = 28
```

或：

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
let count = values.length;
values = values.reduce((previous, current) => current += previous);
values /= count;
// avg = 28
```

現在，如果要取得中間值的步驟：
- 將陣列排序
- 取得中間值的算術平均值

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
values.sort((a, b) => a - b);
let lowMiddle = Math.floor((values.length - 1) / 2);
let highMiddle = Math.ceil((values.length - 1) / 2);
let median = (values[lowMiddle] + values[highMiddle]) / 2;
// median = 13,5
```

隨著位元運算符：

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
values.sort((a, b) => a - b);
let median = (values[(values.length - 1) >> 1] + values[values.length >> 1]) / 2
// median = 13,5
```
