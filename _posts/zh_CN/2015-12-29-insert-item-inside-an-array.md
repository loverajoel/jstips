---
layout: post

title: 向数组中插入元素
tip-number: 00
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: 向一个数组中插入元素是平时很常见的一件事情。你可以使用push在数组尾部插入元素,可以用unshift在数组头部插入元素,也可以用splice在数组中间插入元素。


categories:
    - zh_CN
---

向一个数组中插入元素是平时很常见的一件事情。你可以使用push在数组尾部插入元素,可以用unshift在数组头部插入元素,也可以用splice在数组中间插入元素。

但是这些已知的方法，并不意味着没有更加高效的方法。让我们接着往下看……

向数组结尾添加元素用push()很简单，但下面有一个更高效的方法

```javascript
var arr = [1,2,3,4,5];

arr.push(6);

arr[arr.length] = 6; // 在Mac OS X 10.11.1下的Chrome 47.0.2526.106中快43%
```
两种方法都是修改原始数组。不信？看看[jsperf](http://jsperf.com/push-item-inside-an-array)

现在我们试着向数组的头部添加元素：

```javascript
var arr = [1,2,3,4,5];

arr.unshift(0);

[0].concat(arr); // 在Mac OS X 10.11.1下的Chrome 47.0.2526.106中快98%
```
这里有一些小区别，unshift操作的是原始数组，concat返回一个新数组，参考[jsperf](http://jsperf.com/unshift-item-inside-an-array)

使用splice可以简单的向数组中间添加元素，这也是最高效的方法。

```javascript
var items = ['one', 'two', 'three', 'four'];
items.splice(items.length / 2, 0, 'hello');
```


我在许多浏览器和系统中进行了测试，结果都是相似的。希望这条小知识可以帮到你，也欢迎大家自行测试。
