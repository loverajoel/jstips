---
layout: post

title: 赋值技巧
tip-number: 35
tip-username: hsleonis
tip-username-profile: https://github.com/hsleonis
tip-tldr: 赋值是很常见的。有时候打字对于我们这些“懒惰的程序员”来说是很费时间的。所以，我们可以使用一些小把戏来使我们的代码更清楚更简单。

redirect_from:
  - /zh_cn/assignment-shorthands/

categories:
    - zh_CN
    - javascript
---

赋值是很常见的。有时候打字对于我们这些“懒惰的程序员”来说是很费时间的。
所以，我们可以使用一些小把戏来使我们的代码更清楚更简单。

这类似于使用：

```js
x += 23; // x = x + 23;
y -= 15; // y = y - 15;
z *= 10; // z = z * 10;
k /= 7; // k = k / 7;
p %= 3; // p = p % 3;
d **= 2; // d = d ** 2;
m >>= 2; // m = m >> 2;
n <<= 2; // n = n << 2;
n ++; // n = n + 1;
n --; n = n - 1;

```

### `++` 与 `--` 操作符

对于`++`操作符有些特殊。最好用下面的例子解释一下：

```js
var a = 2;
var b = a++;
// 现在 a == 3  b == 2
```

`a++`做了如下工作：
  1. 返回`a`的值
  2. `a`增加1

但是如果我们想让值先增加呢？这也很容易：

```js
var a = 2;
var b = ++a;
// 现在a和b都是3
```

看明白了吗？我将操作符放在了参数_前面_。

`--`操作符除了使值减小外，其他功能是类似的。

### If-else (使用三元运算符)

我们平时会这样写：

```js
var newValue;
if(value > 10) 
  newValue = 5;
else
  newValue = 2;
```

我们可以使用三元运算符是它更简便：

```js
var newValue = (value > 10) ? 5 : 2;
```

### 检测Null、Undefined、空

```js
if (variable1 !== null || variable1 !== undefined || variable1 !== '') {
     var variable2 = variable1;
}
```

简便写法：

```js
var variable2 = variable1  || '';
```

P.S.：如果`variable1`是一个数字，则先检查他是否为0。

### 对象数组表示法

不要用：

```js
var a = new Array();
a[0] = "myString1";
a[1] = "myString2";
```

使用：

```js
var a = ["myString1", "myString2"];
```

### 关联数组

不要用：

```js
var skillSet = new Array();
skillSet['Document language'] = 'HTML5';
skillSet['Styling language'] = 'CSS3';
```

使用：

```js
var skillSet = {
    'Document language' : 'HTML5', 
    'Styling language' : 'CSS3'
};
```
