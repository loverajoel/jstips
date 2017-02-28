---
layout: post

title: 在陣列中加入元素
tip-number: 00
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: 在一個存在的陣列加入新的元素是一件很常見的事情，你可以使用 push 將元素加入到陣列的末端，或是使用 unshift 在陣列起始位置加入元素，也可以使用 splice 在陣列中間的地方加入元素。
tip-writer-support: https://www.coinbase.com/loverajoel


redirect_from:
  - /zh_tw/insert-item-inside-an-array/
  
categories:
    - zh_TW
    - javascript
---

# 在存在的陣列加入新的元素

在一個存在的陣列加入新的元素是一件很常見的事情，你可以使用 push 將元素加入到陣列的末端，或是使用 unshift 在陣列起始位置加入元素，也可以使用 splice 在陣列中間的地方加入元素。

那些都是已知的方法，但這並不代表沒有更好的效能的方法。讓我們開始吧:

## 在陣列最後加入新的元素

在陣列最後加入新的元素我們可以簡單地透過 push() 方式，但以下是更能提升效能方法。

```javascript
var arr = [1, 2, 3, 4, 5];
var arr2 = [];

arr.push(6);
arr[arr.length] = 6;
arr2 = arr.concat([6]);
```
這兩種方法都是修改原始的陣列。不相信嗎？請參考 [jsperf](http://jsperf.com/push-item-inside-an-array)。

### 在 mobile 上的性能表現：

#### Android (v4.2.2)

1. _arr.push(6);_ 和 _arr[arr.length] = 6;_ 有相同的性能表現 // 3 319 694 ops/sec
3. _arr2 = arr.concat([6]);_ 較以上兩個方法慢 50.61 %

#### Chrome Mobile (v33.0.0)

1. _arr[arr.length] = 6;_ // 6 125 975 ops/sec
2. _arr.push(6);_ 慢 66.74 %
3. _arr2 = arr.concat([6]);_ 慢 87.63 %

#### Safari Mobile (v9)

1. _arr[arr.length] = 6;_ // 7 452 898 ops/sec
2. _arr.push(6);_ 慢 40.19 %
3. _arr2 = arr.concat([6]);_ 慢 49.78 %

```javascript
最後勝利者

1. arr[arr.length] = 6; // 平均 5 632 856 ops/sec
2. arr.push(6); // 慢 35.64 %
3. arr2 = arr.concat([6]); // 慢 62.67 %
```

### 在 desktop 的性能表現

#### Chrome (v48.0.2564)

1. _arr[arr.length] = 6;_ // 21 602 722 ops/sec
2. _arr.push(6);_ 慢 61.94 %
3. _arr2 = arr.concat([6]);_ 慢 87.45 %

#### Firefox (v44)

1. _arr.push(6);_ // 56 032 805 ops/sec
2. _arr[arr.length] = 6;_ 慢 0.52 %
3. _arr2 = arr.concat([6]);_ 慢 87.36 %

#### IE (v11)

1. _arr[arr.length] = 6;_ // 67 197 046 ops/sec
2. _arr.push(6);_ 慢 39.61 %
3. _arr2 = arr.concat([6]);_ 慢 93.41 %

#### Opera (v35.0.2066.68)

1. _arr[arr.length] = 6;_ // 30 775 071 ops/sec
2. _arr.push(6);_ 慢 71.60 %
3. _arr2 = arr.concat([6]);_ 慢 83.70 %

#### Safari (v9.0.3)

1. _arr.push(6);_ // 42 670 978 ops/sec
2. _arr[arr.length] = 6;_ 慢 0.80 %
3. _arr2 = arr.concat([6]);_ 慢 76.07 %

```javascript
最後勝利者

1. arr[arr.length] = 6; // 平均 42 345 449 ops/sec
2. arr.push(6); // 慢 34.66 %
3. arr2 = arr.concat([6]); // 慢 85.79 %
```

## 在陣列起始加入元素

現在我們嘗試在陣列的起始加入元素：

```javascript
var arr = [1, 2, 3, 4, 5];

arr.unshift(0);
[0].concat(arr);
```
這裡有更多小細項：unshift 修改原始陣列；concat 回傳一個新的陣列。[jsperf](http://jsperf.com/unshift-item-inside-an-array)

### 在 mobile 的性能表現：

#### Android (v4.2.2)

1. _[0].concat(arr);_ // 1 808 717 ops/sec
2. _arr.unshift(0);_ 慢 97.85 %

#### Chrome Mobile (v33.0.0)

1. _[0].concat(arr);_ // 1 269 498 ops/sec
2. _arr.unshift(0);_ 慢 99.86 %

#### Safari Mobile (v9)

1. _arr.unshift(0);_ // 3 250 184 ops/sec
2. _[0].concat(arr);_ 慢 33.67 %

```javascript
最後勝利者

1. [0].concat(arr); // 平均 4 972 622 ops/sec
2. arr.unshift(0); // 慢 64.70 %
```

### 在 desktop 的性能表現

#### Chrome (v48.0.2564)

1. _[0].concat(arr);_ // 2 656 685 ops/sec
2. _arr.unshift(0);_ 慢 96.77 %

#### Firefox (v44)

1. _[0].concat(arr);_ // 8 039 759 ops/sec
2. _arr.unshift(0);_ 慢 99.72 %

#### IE (v11)

1. _[0].concat(arr);_ // 3 604 226 ops/sec
2. _arr.unshift(0);_ 慢 98.31 %

#### Opera (v35.0.2066.68)

1. _[0].concat(arr);_ // 4 102 128 ops/sec
2. _arr.unshift(0);_ 慢 97.44 %

#### Safari (v9.0.3)

1. _arr.unshift(0);_ // 12 356 477 ops/sec
2. _[0].concat(arr);_ 慢 15.17 %

```javascript
最後勝利者

1. [0].concat(arr); // 平均 6 032 573 ops/sec
2. arr.unshift(0); // 慢 78.65 %
```

## 在陣列中間加入元素

在陣列中間可以簡單透過 splice 來加入元素，這樣的做法是最具效能的方式。

```javascript
var items = ['one', 'two', 'three', 'four'];
items.splice(items.length / 2, 0, 'hello');
```

我嘗試在不同的瀏覽器和 OS 執行這些測試，他們的結果是相似的。我希望這些知識對你是有幫助的，也鼓勵你自己進行測試！