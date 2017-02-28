---
layout: post

title: 透過 Map() 在你的物件屬性加入排序
tip-number: 32
tip-username: loverajoel
tip-username-profile: https://twitter.com/loverajoel
tip-tldr: 物件是一個沒有排序的屬性集合...意思說，如果你想嘗試在你的物件儲存已排序的資料，你需要重新檢查，因為屬性在物件不保證是有排序的。
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /zh_tw/map-to-the-rescue-adding-order-to-object-properties/

categories:
    - zh_TW
    - javascript
---

## 物件屬性的順序

> 一個物件是一個 `Object` 的類型。它是包含原始值、物件、或是函式這些尚未排序屬性的集合。一個物件的屬性儲存了一個函式稱為方法。 [ECMAScript](http://www.ecma-international.org/publications/files/ECMA-ST-ARCH/ECMA-262,%203rd%20edition,%20December%201999.pdf)

實際看一下範例

```js
var myObject = {
	z: 1,
	'@': 2,
	b: 3,
	1: 4,
	5: 5
};
console.log(myObject) // Object {1: 4, 5: 5, z: 1, @: 2, b: 3}

for (item in myObject) {...
// 1
// 5
// z
// @
// b
```
因為每個瀏覽器有自己排序物件的規則，所以順序是不確定的。

## 要如何解決這個問題？

### Map

使用 ES6 的新特性 - Map。[Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) 物件迭代元素插入的順序。`for...of` 迴圈每次迭代回傳一個 [key, value] 的陣列。

```js
var myObject = new Map();
myObject.set('z', 1);
myObject.set('@', 2);
myObject.set('b', 3);
for (var [key, value] of myObject) {
  console.log(key, value);
...
// z 1
// @ 2
// b 3
```

### 對舊的瀏覽器 Hack

Mozilla 建議：
> 所以，如果你想要在跨瀏覽器的環境模擬一個有排序的關聯陣列，你要麼強制使用兩個分離的陣列（其中一個給 keys，另一個給 values），或者建立一個單一屬性的物件陣列，等等。

```js
// 使用兩個分離的陣列
var objectKeys = [z, @, b, 1, 5];
for (item in objectKeys) {
	myObject[item]
...

// 建立一個單一屬性的物件陣列
var myData = [{z: 1}, {'@': 2}, {b: 3}, {1: 4}, {5: 5}];
```
