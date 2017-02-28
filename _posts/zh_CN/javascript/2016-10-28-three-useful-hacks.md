---
layout: post

title: 三个实用的javascript小技巧
tip-number: 60
tip-username: leandrosimoes
tip-username-profile: https://github.com/leandrosimoes
tip-tldr: 分享三个让开发变得更高效的实用语法糖


redirect_from:
  - /zh_cn/three-useful-hacks/

categories:
    - zh_CN
    - javascript
---

#### 从后向前获取数组元素

如果你想从后向前获取一个数组的元素，可以这样写：

```javascript
var newArray = [1, 2, 3, 4]

console.log(newArray.slice(-1)) // [4]
console.log(newArray.slice(-2)) // [3, 4]
console.log(newArray.slice(-3)) // [2, 3, 4]
console.log(newArray.slice(-4)) // [1, 2, 3, 4]
```

#### 短路条件句

如果你想在某个条件逻辑值为`true`时，执行某个函数，就像这样：

```javascript
if (condition) {
  dosomething()
}
```

这时，你可以这样子运用短路：

```javascript
condition && dosomething()
```

#### 用操作符 "||" 来设置默认值

如果你必须给一个变量赋默认值，可以简单的这样写：

```javascript
var a

console.log(a) // undefined

a = a || 'default value'

console.log(a) // default value

a = a || 'new value'

console.log(a) // default value
```
