---
layout: post

title: break 或 continue 循环函数
tip-number: 58
tip-username: vamshisuram
tip-username-profile: https://github.com/vamshisuram
tip-tldr: 循环一个`list`从中寻找一个或一些值，是一个很常见的需求。但是即使我们要找的元素就是数组里的第一个，我们不也能从循环中直接`return`，只能遍历整个数组。本文教你如何使用`.some`和`.every`快速结束循环。


redirect_from:
  - /zh_cn/break-continue-loop-functional/

categories:
    - zh_CN
    - javascript
---


停止循环是循环中一个常见的需求。使用`for`循环我们可以用`break`提前结束循环。

```javascript
const a = [0, 1, 2, 3, 4];
for (var i = 0; i < a.length; i++) {
  if (a[i] === 2) {
    break; // stop the loop
  }
  console.log(a[i]);
}
//> 0, 1
```

另一个常见的需求使我们需要直接取得变量。

一个快速的方式是使用`.forEach`，但是这样我们就失去了`break`的能力。这种情况下，最接近的方式是使用`return`实现`continue`的功能。

```javascript
[0, 1, 2, 3, 4].forEach(function(val, i) {
  if (val === 2) {
    // 怎么停止呢?
    return true;
  }
  console.log(val); // your code
});
//> 0, 1, 3, 4
```

`.some`是一个原型方法。他用来检测是否某些元素满足所提供的函数。如果任何元素最终返回`true`，它就会停止运行。更多解释请看[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/some)。

引子上面链接的一个例子：

```javascript
const isBiggerThan10 = numb => numb > 10;

[2, 5, 8, 1, 4].some(isBiggerThan10);  // false
[12, 5, 8, 1, 4].some(isBiggerThan10); // true
```

使用`.some`我们拥有了类似`.forEach`的功能，而且使用`return`实现了`break`的效果。

```javascript
[0, 1, 2, 3, 4].some(function(val, i) {
  if (val === 2) {
    return true;
  }
  console.log(val); // your code
});
//> 0, 1
```


你可以返回`false`使循环`continue`到下一个元素。当你返回`true`时，循环将会`break`，此时`a.some(..)`将会`return` `true`。

```javascript
// Array contains 2
const isTwoPresent = [0, 1, 2, 3, 4].some(function(val, i) {
  if (val === 2) {
    return true; // break
  }
});
console.log(isTwoPresent);
//> true
```

还有`.every`函数同样可以实现此功能。但此时我们需要返回与`.some`相反的布尔值。

##### 示例
<div>
  <a class="jsbin-embed" href="http://jsbin.com/jopeji/embed?js,console">JS Bin on jsbin.com</a><script src="http://static.jsbin.com/js/embed.min.js?3.39.11"></script>
</div>
