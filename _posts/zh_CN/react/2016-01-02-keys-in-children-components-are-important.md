---
layout: post

title: 子容器的Key是很重要的
tip-number: 02
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: key是必须传递给从数组中动态创建的所有组件的一个值。它是一个唯一且固定的id，用来识别DOM中的每个组件，也可以让我们区别它是否是同一个组件。使用key可以确保子容器是可保存而且不需要重复创建的，还可以防止奇怪的事情发生。
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /zh_cn/keys-in-children-components-are-important/

categories:
    - zh_CN
    - react
---

[key](https://facebook.github.io/react/docs/multiple-components.html#dynamic-children)必须传递给从数组中动态创建的所有组件的一个值。它是一个唯一且固定的id，用来识别DOM中的每个组件，也可以让我们区别它是否是同一个组件。使用key可以确保子容器是可保存而且不需要重复创建的，还可以防止奇怪的事情发生。

> key跟效率不是很相关，它更与身份有关系（这间接的使效率更好）。随机的赋值或改变值将不能识别身份[Paul O’Shannessy](https://github.com/facebook/react/issues/1342#issuecomment-39230939)

- 使用对象存在的的唯一值。
- 在父组件定义key,而不是子组件。

```javascript
//bad
...
render() {
	<div key={% raw %}{{item.key}}{% endraw %}>{% raw %}{{item.name}}{% endraw %}</div>
}
...

//good
<MyComponent key={% raw %}{{item.key}}{% endraw %}/>
```

- [使用数组索引是一个坏习惯](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318#.76co046o9)
- `random()` 不会起作用

```javascript
//bad
<MyComponent key={% raw %}{{Math.random()}}{% endraw %}/>
```

- 你可以创建以自己的唯一id。确定这个方法运行速度够快，把它附着到你的对象上。
- 当子组件的数量很大或者包含重量级的组件时，使用key来提高性能。
- [你必须提供key值给ReactCSSTransitionGroup的每个子组件](http://docs.reactjs-china.com/react/docs/animation.html)