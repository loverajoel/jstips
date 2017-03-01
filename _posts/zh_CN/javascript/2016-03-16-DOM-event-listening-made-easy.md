---
layout: post

title: 简单监听DOM事件
tip-number: 51
tip-username: octopitus
tip-username-profile: https://github.com/octopitus
tip-tldr: 简单而优雅地操作DOM事件的方法

redirect_from:
  - /zh_cn/DOM-event-listening-made-easy/

categories:
    - zh_CN
    - javascript
---
很多人还在这样做：

- `element.addEventListener('type', obj.method.bind(obj))`
- `element.addEventListener('type', function (event) {})`
- `element.addEventListener('type', (event) => {})`

上面所有的例子都创建了一个匿名事件监控句柄，且在不需要时无法删除它。这在你不需要某句柄，而它却被用户或[事件冒泡](http://www.javascripter.net/faq/eventbubbling.htm)偶然触发时，可能会导致性能问题或不必要的逻辑问题。

更安全的事件处理方式如下：

使用引用：

```js
const handler = function () {
  console.log("Tada!")
}
element.addEventListener("click", handler)
// 之后
element.removeEventListener("click", handler)
```

命名的函数移除它本身:

```js
element.addEventListener('click', function click(e) {
  if (someCondition) {
    return e.currentTarget.removeEventListener('click', click);
  }
});
```

更好的写法：

```js
function handleEvent (eventName, {onElement, withCallback, useCapture = false} = {}, thisArg) {
  const element = onElement || document.documentElement

  function handler (event) {
    if (typeof withCallback === 'function') {
      withCallback.call(thisArg, event)
    }
  }

  handler.destroy = function () {
    return element.removeEventListener(eventName, handler, useCapture)
  }

  element.addEventListener(eventName, handler, useCapture)
  return handler
}

// 你需要的时候
const handleClick = handleEvent('click', {
  onElement: element,
  withCallback: (event) => {
    console.log('Tada!')
  }
})

// 你想删除它的时候
handleClick.destroy()
```
