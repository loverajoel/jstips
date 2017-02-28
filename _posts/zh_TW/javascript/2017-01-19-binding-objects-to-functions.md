---
layout: post

title: Bind 物件到 function
tip-number: 61
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: 了解在 JavaScript 中如何使用 `Bind` 方法和物件以及 function


redirect_from:
  - /zh_tw/binding-objects-to-functions/

categories:
    - zh_TW
    - javascript
---

很多時候，我們需要 bind 一個物件到一個 function 的 this 物件。當 this 明確的被指定在 JS 的 bind 方法且我們需要調用所需的方法。

### Bind 語法

```js
fun.bind(thisArg[, arg1[, arg2[, ...]]])
```

## 參數
**thisArg**

`this` 參數值可以被傳送到目標的 function 同時呼叫 被 `bind` 的 function。

**arg1, arg2, ...**

前置參數被傳送到被 `bind` 的 function 同時調用目標 function。

**回傳值**

一個給定 function 的副本以及指定的 `this` 值和初始參數。

### 在 JS 的 action 中 Bind 方法

```js
const myCar = {
 brand: 'Ford',
 type: 'Sedan'
 Color: ‘Red’
};

const getBrand = () => {
 console.log(this.brand);
};

const getType = () => {
 console.log(this.type);
};

const getColor = () => {
 console.log(this.color);
};

getBrand(); // 物件沒有被 bind，undefined

getBrand(myCar); // 物件沒有被 bind，undefined

getType.bind(myCar)(); // Sedan

getColor.bind(myCar); // Red

```
