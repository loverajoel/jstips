---
layout: post

title: 仅用一行生成0...N的数列
tip-number: 33
tip-username: SarjuHansaliya
tip-username-profile: https://github.com/SarjuHansaliya
tip-tldr: 我们可以创建一个函数，它可以仅用一行代码生成0...N数列。


categories:
    - zh_CN
---

使用下面一行代码，我们就可以生成0...N数列。

```js
Array.apply(null, {length: N}).map(Number.call, Number);
```

让我们把这一行拆分一下。我们知道"call"方法在Javascript中的作用。"call"方法的第一个参数是上下文，从第二个参数开始是调用"call"方法的函数所需要的参数。

```js
function add(a,b){
    return (a+b);
}
add.call(null,5,6);
```
这将返回5加6的和。

数组的map接收两个参数，第一个是回调函数(callback)，第二个是上下文(this)。回调函数接收三个参数：`value` 、`index`和我们正在迭代的整个数组。所以正常的语法就像：

```js
[1,2,3].map(function(val,index,arr){
    //Code
},this);
```
如下一行创建了一个所给长度(length)的数组：

```js
Array.apply(null, {length: N})
```
将各部分合并就成了如下解决方案：

```js
Array.apply(null, {length: N}).map(Number.call, Number);
```

如果你需要1...N的数列，你可以这样写：

```js
Array.apply(null, {length: N}).map(function(val,index){
  return index+1;  
});
```