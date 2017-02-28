---
layout: post

title: AngularJs - $digest vs $apply
tip-number: 01
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: JavaScript模块和构建步骤越来越复杂和多样化，但是新框架里的样板是什么样子的呢？
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /zh_cn/angularjs-digest-vs-apply/

categories:
    - zh_CN
    - angular
---

AngularJs最令人欣赏的特性之一就是双向数据绑定。AngularJs通过循环(`$digest`)检查model和view的变化实现此功能。想要理解框架底层的运行机制你需要理解这个概念。

当一个事件被触发时，Angular触发每个watcher. 这是我们已知的`$digest`循环。有时你需要强制手动运行一个新的循环，而且因为这是最影响性能的一方面，你必须选择一个正确的选项。

### `$apply`
这个核心方法可以让你显式启动`digest`循环。这意味着所有的watcher将会被检测；整个应用启动`$digest loop`。在内部在会执行一个可选的方法之后，会调用`$rootScope.$digest();`.

### `$digest`
这种情况下`$digest`方法在当前作用域和它的子作用域启动`$digest`循环。你需要注意他的父作用域将不会被检测也不会被影响。

### 推荐
- 仅当浏览器DOM事件在AngularJS之外被触发时使用`$apply`或`$digest`。
- 给`$apply`传递方法，它将包含错误处理机制而且允许整合在`digest`循环里的变化。

```javascript
$scope.$apply(() => {
	$scope.tip = 'Javascript Tip';
});
```

- 如果你只需要更新当前的作用域或者它的子作用域的话，使用`$digest`，而且要防止在整个应用里运行新的`digest`循环。这在性能上的好处是显而易见的。
- `$apply()`对机器来说是一个困难的处理过程，在绑定过多的时候可能会引发性能问题。
- 如果你正使用`>AngularJS 1.2.X`版本，使用`$evalAsync`, 这个方法将在当前循环或下一个循环执行表达式，这能提高你的应用的性能。
