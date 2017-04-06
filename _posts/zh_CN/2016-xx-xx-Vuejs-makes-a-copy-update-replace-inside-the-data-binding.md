---
layout: post

title: Vuejs在数据绑定时会复制更新并替换目标元素
tip-number: 60
tip-username: pansila
tip-username-profile: https://github.com/pansila
tip-tldr: 在这个提示中，我会通过一个例子向您展示Vue会如何与其它软件冲突如果你不知道这一点。

categories:
    - zh_CN
---

### 概述

Vuejs是一款简单而强大的软件杰作，类似其它流行的UI框架，Angularjs和Reactjs，但不像这两者令人生畏的复杂性，Vue非常简单，在从入门到放弃之前，你能很快掌握它的全部知识并投入生产。

但是如果你不知道它怎么工作的，有时候它也会难为你。这里是一个和其它UI框架(Framework7)冲突的例子。

```html
<!-- index.html -->
<div class="pages">
  <div class="page" date-page="index">
    <!-- load a new page -->
    <a href="test.html">new page</a>
  </div>
</div>

<!-- test.html -->
<div class="pages">
	<div class="page" date-page="test" id="test">
	  <div class="page-content" id="test1">
		<p>{{content}}</p>
	  </div>
	</div>
</div>
```

```js
var myApp = new Framework7();
myApp.onPageInit('test', function (page) {
  new Vue({
    el: '#test',
    data: {
      content: 'hello world'
    }
  });
});
```

你可能会惊讶它竟然无法工作，新的page点击后并没有显示出来。事实上，Vue内部会复制目标HTML元素，然后根据绑定的数据更新并替换原来的元素。当Framework7加载新的页面时，它会调用`PageInit`回调函数，这里我们又调用了Vue在`<page>`元素上进行数据绑定，这之后DOM树里面包含的已经是新的`<page>`元素，但Framework7对此并不知情又接着在旧的`<page>`元素上完成剩下的初始化工作，比如最终显示这个新的页面，这就是根本原因。

为了绕过这个问题，不要让Vue的元素选择器锚定在`<page>`元素上，而是定在它的子元素，这样Vue做数据绑定时就不会影响到整个页面显示。

```js
var myApp = new Framework7();
myApp.onPageInit('test', function (page) {
  new Vue({
    el: '#test1',
    data: {
      content: 'hello world'
    }
  })
})
```

### 更多信息

- [Vue](https://github.com/Vuejs/Vue)
- [Vue教程] (https://cn.vuejs.org/)
- [Framework7](https://framework7.io/)
