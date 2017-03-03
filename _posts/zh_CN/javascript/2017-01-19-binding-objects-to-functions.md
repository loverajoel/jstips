---
layout: post

title: 给函数 Bind 对象
tip-number: 61
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: 理解在 JavaScript 中如何使用 `Bind` 方法绑定对象和函数


redirect_from:
  - /zh_cn/binding-objects-to-functions/

categories:
    - zh_CN
    - javascript
---

我们常常需要将一个对象绑定到一个方法的 `this` 上。在 JS 中，如果你想要调用一个函数并指定它的 `this` 时可以使用 `bind` 方法。

### Bind 语法

```js
fun.bind(thisArg[, arg1[, arg2[, ...]]])
```

## 参数
**thisArg**

当绑定函数被调用时，该参数会作为原函数运行时的 this 指向。

**arg1, arg2, ...**

当绑定函数被调用时，这些参数将置于实参之前传递给被绑定的方法。

**返回值**

返回由指定的this值和初始化参数改造的原函数拷贝

### JS 中的实例

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

getBrand(); // object not bind,undefined

getBrand(myCar); // object not bind,undefined

getType.bind(myCar)(); // Sedan

getColor.bind(myCar); // Red

```