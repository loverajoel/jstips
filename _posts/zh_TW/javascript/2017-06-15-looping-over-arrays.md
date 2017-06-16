---
layout: post

title: 循環陣列
tip-number: 79
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: 這裡有一些方法在 JavaScript 中可以循環陣列。我們將從典型例子並且補充標準規範。

categories:
    - zh_TW
    - javascript
---

這裡有一些方法在 JavaScript 中可以循環陣列。我們將從典型例子並且補充標準規範。

## while

```javascript
let index = 0;
const array = [1,2,3,4,5,6];

while (index < array.length) {
  console.log(array[index]);
  index++;
}
```

## for（典型）

```javascript
const array = [1,2,3,4,5,6];
for (let index = 0; index < array.length, index++) {
  console.log(array[index]);
}
```

## forEach

```javascript
const array = [1,2,3,4,5,6];

array.forEach(function(current_value, index, array) {
  console.log(`At index ${index} in array ${array} the value is ${current_value}`);
});
// => undefined
```

## map

最後的 construct 很有用，然而，它不會回傳一個新的陣列，這可能對你指定的情況是不合乎的。`map` 透過對每個元素應用一個函式，並回傳新的陣列來解決問題。

```javascript
const array = [1,2,3,4,5,6];
const square = x => Math.pow(x, 2);
const squares = array.map(square);
console.log(`Original array: ${array}`);
console.log(`Squared array: ${array}`);
```

`map` 完整個宣告方式：`.map(current_value, index, array)`。

## reduce

根據 MDN：

> reduce() 方法對累加器和數組中的每個元素（從左到右）應用一個函式，將其減少為一個值。

```javascript
const array = [1,2,3,4,5,6];
const sum = (x, y) => x + y;
const array_sum = array.reduce(sum, 0);
console.log(`The sum of array: ${array} is ${array_sum}`);
```


## filter

基於一個布林函式對陣列進行過濾。

```javascript
const array = [1,2,3,4,5,6];
const even = x => x % 2 === 0;
const even_array = array.filter(even);
console.log(`Even numbers in array ${array}: ${even_array}`);
```

## every

取得一個陣列，並且想要測試每個元素中是否滿足給定的條件？

```javascript
const array = [1,2,3,4,5,6];
const under_seven = x => x < 7;

if (array.every(under_seven)) {
  console.log('Every element in the array is less than 7');
} else {
  console.log('At least one element in the array was bigger than 7');
}
```

## some

測試至少一個元素是否 match 我們的布林函式。

```javascript
const array = [1,2,3,9,5,6,4];
const over_seven = x => x > 7;

if (array.some(over_seven)) {
  console.log('At least one element bigger than 7 was found');
} else {
  console.log('No element bigger than 7 was found');
}
```
