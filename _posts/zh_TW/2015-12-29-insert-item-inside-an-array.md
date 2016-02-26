---
layout: post

title: 在陣列中加入元素
tip-number: 00
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: 在一個存在的陣列加入新的元素是一件很常見的事情，你可以使用 push 將元素加入到陣列的末端，或是使用 unshift 在陣列起始位置加入元素，也可以使用 slice 在陣列中間的地方加入元素。


categories:
    - zh_TW
---

在一個存在的陣列加入新的元素是一件很常見的事情，你可以使用 push 將元素加入到陣列的末端，或是使用 unshift 在陣列起始位置加入元素，也可以使用 slice 在陣列中間的地方加入元素。

那些都是已知的方法，但這並不代表沒有更好的效能的方法。讓我們開始吧:

在陣列的末端加入元素我們可以簡單地透過 push() 方式，但以下是更能提升效能方法。

```javascript
var arr = [1, 2, 3, 4, 5];

arr.push(6);
arr[arr.length] = 6; // 在 Mac OS X 10.11.1 下的 Chrome 47.0.2526.106 加快了 43%
```
這兩種方法都是修改原始的陣列。不相信嗎？請參考 [jsperf](http://jsperf.com/push-item-inside-an-array)。

現在，如果我們要嘗試在陣列的起始位置加入元素：

```javascript
var arr = [1, 2, 3, 4, 5];

arr.unshift(0);
[0].concat(arr); // 在 Mac OS X 10.11.1 下的 Chrome 47.0.2526.106 加快了 98%
```
這裡有更多的小細節：使用 unshift 修改原始的陣列；concat 返回新的陣列。 [jsperf](http://jsperf.com/unshift-item-inside-an-array)

使用 splice 陣列的中間加入元素是相當容易的，而且是最高效的方法。

```javascript
var items = ['one', 'two', 'three', 'four'];
items.splice(items.length / 2, 0, 'hello');
```

我嘗試在不同的瀏覽器和 OS 執行這些測試，他們的結果是相似的。我希望這些知識對你是有幫助的，也鼓勵你自己進行測試！
