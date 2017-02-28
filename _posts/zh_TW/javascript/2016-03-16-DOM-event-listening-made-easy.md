---
layout: post

title: 簡單的監聽 DOM 事件
tip-number: 51
tip-username: octopitus
tip-username-profile: https://github.com/octopitus
tip-tldr: 一個優雅和簡單的方式來處理 DOM 事件。

redirect_from:
  - /zh_tw/DOM-event-listening-made-easy/

categories:
    - zh_TW
    - javascript
---
很多人仍然透過以下方法來處理 DOM 事件︰

- `element.addEventListener('type', obj.method.bind(obj))`
- `element.addEventListener('type', function (event) {})`
- `element.addEventListener('type', (event) => {})`

當你不需要這些處理函式時，使用者可能因為交互事件或[冒泡事件](http://www.javascripter.net/faq/eventbubbling.htm)而不小心觸發意外。

安全的事件處理模式包含以下這些：

使用一個參考：

```js
const handler = function () {
  console.log("Tada!")
}
element.addEventListener("click", handler)
// 之後
element.removeEventListener("click", handler)
```

命名函式刪除本身：

```js
element.addEventListener('click', function click(e) {
  if (someCondition) {
    return e.currentTarget.removeEventListener('click', click);
  }
});
```

更好的方式：

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

// 任何你需要的時候
const handleClick = handleEvent('click', {
  onElement: element,
  withCallback: (event) => {
    console.log('Tada!')
  }
})

// 任何時候你想要將它移除
handleClick.destroy()
```
