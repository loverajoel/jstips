---
layout: post

title: 更快的取整
tip-number: 18
tip-username: pklinger
tip-username-profile: https://github.com/pklinger
tip-tldr: 今天的小知识有关性能表现。曾经用过双波浪`~~` 操作符吗? 有时候也称为双非(NOT)位操作. 你可以用它作为`Math.floor()`的替代方法。为什么会这样呢?

categories:
    - zh_CN
---

今天的小知识有关性能表现。[曾经用过双波浪](http://stackoverflow.com/questions/5971645/what-is-the-double-tilde-operator-in-javascript) `~~` 操作符吗? 有时候也称为双非(NOT)位操作. 你可以用它作为`Math.floor()`的替代方法。为什么会这样呢?

一个位操作符 `~` 将输入的32位的数字(input)转换为 `-(input+1)`. 两个位操作符将输入(input)转变为 `-(-(input + 1)+1)` 是一个使结果趋向于0的取整好工具. 对于数字, 负数就像使用`Math.ceil()`方法而正数就像使用`Math.floor()`方法. 转换失败时,返回`0`,这在`Math.floor()`方法转换失败返回`NaN`时或许会派上用场。

```javascript
// 单个 ~
console.log(~1337)    // -1338

// 数字输入
console.log(~~47.11)  // -> 47
console.log(~~-12.88) // -> -12
console.log(~~1.9999) // -> 1
console.log(~~3)      // -> 3

// 转换失败
console.log(~~[]) // -> 0
console.log(~~NaN)  // -> 0
console.log(~~null) // -> 0

// 大于32位整数时转换失败
console.log(~~(2147483647 + 1) === (2147483647 + 1)) // -> 0
```

虽然`~~`的性能更好,为了代码的可读性请用`Math.floor()`.
