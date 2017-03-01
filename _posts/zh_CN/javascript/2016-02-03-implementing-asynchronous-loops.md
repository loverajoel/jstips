---
layout: post

title: 实现异步循环
tip-number: 34
tip-username: madmantalking
tip-username-profile: https://github.com/madmantalking
tip-tldr: 实现异步循环时，你可能会遇到问题。 

redirect_from:
  - /zh_cn/implementing-asynchronous-loops/

categories:
    - zh_CN
    - javascript
---

让我们试着写一个异步方法，每秒打印一次循环的索引值。

```js
for (var i=0; i<5; i++) {
	setTimeout(function(){
		console.log(i); 
	}, 1000 * (i+1));
}  
```

如上程序的输出为：

```js
> 5
> 5
> 5
> 5
> 5
```

这明显是有问题的。

**原因**

每次时间结束(timeout)都指向原始的`i`，而并非它的拷贝。所以，for循环使`i`增长到5，之后`timeout`运行并调用了当前`i`的值（也就是5）。

好吧，这个问题看起来很简单。最直接的解决方法是将循环的索引缓存在一个临时变量里。

```js
for (var i=0; i<5; i++) {
	var temp = i;
 	setTimeout(function(){
		console.log(temp); 
	}, 1000 * (i+1));
}  
```

但是再次运行，如上的程序输出为：

```js
> 4
> 4
> 4
> 4
> 4
```

这仍然有问题，这是因为并不存在块作用域，而且变量的声明被提升到了作用域顶端。实际上，如上代码和下面是一样的：

```js
var temp;
for (var i=0; i<5; i++) {
 	temp = i;
	setTimeout(function(){
		console.log(temp); 
  	}, 1000 * (i+1));
}  
```

**解决方法**

有几个不同的方式可以拷贝`i`。最普通且常用方法是通过声明函数来建立一个闭包，并将`i`传给此函数。我们这里使用了自调用函数。

```js
for (var i=0; i<5; i++) {
	(function(num){
		setTimeout(function(){
			console.log(num); 
		}, 1000 * (i+1)); 
	})(i);  
}  
```

在JavaScript里，参数是按值传递给函数的。像`Number`、`Date`和`String`这些原始类型为基本复制。当你们在一个函数内改变它的值，并不影响外面的作用域。但`Object`类型不一样：如果你在函数内部修改了它的参数，将会影响到所有包含该`Object`的作用域内它的参数。

另一种方法是使用`let`。在ES6中的`let`关键字是可以实现的，它和`var`不一样，因为它支持块作用域的。

```js
for (let i=0; i<5; i++) {
	var temp = i;
 	setTimeout(function(){
		console.log(i); 
	}, 1000 * (i+1));
}  
```