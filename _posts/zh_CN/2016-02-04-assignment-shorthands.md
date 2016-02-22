---
layout: post

title: 赋值技巧
tip-number: 35
tip-username: hsleonis
tip-username-profile: https://github.com/hsleonis
tip-tldr: 赋值是很常见的。有时候打字对于我们这些“懒惰的程序员”来说是很费时间的。所以，我们可以使用一些小把戏来使我们的代码更清楚更简单。

categories:
    - zh_CN
---

赋值是很常见的。有时候打字对于我们这些“懒惰的程序员”来说是很费时间的。
所以，我们可以使用一些小把戏来使我们的代码更清楚更简单。

这类似于使用：

````javascript
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

````

### If-else (使用三元运算符)

我们平时会这样写：

````javascript
var newValue;
if(value > 10) 
  newValue = 5;
else
  newValue = 2;
````

我们可以使用三元运算符是它更简便：

````javascript
var newValue = (value > 10) ? 5 : 2;
````

### 检测Null、Undefined、空

````javascript
if (variable1 !== null || variable1 !== undefined || variable1 !== '') {
     var variable2 = variable1;
}
````

简便写法：

````javascript
var variable2 = variable1  || '';
````
P.S.：如果`variable1`是一个数字，则先检查他是否为0。

### 对象数组表示法

不要用：

````javascript
var a = new Array();
a[0] = "myString1";
a[1] = "myString2";
````
使用：

````javascript
var a = ["myString1", "myString2"];
````

### 关联数组

不要用：

````javascript
var skillSet = new Array();
skillSet['Document language'] = 'HTML5';
skillSet['Styling language'] = 'CSS3';
````

使用：

````javascript
var skillSet = {
    'Document language' : 'HTML5', 
    'Styling language' : 'CSS3'
};
````
