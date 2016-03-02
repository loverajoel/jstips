---
layout: *post

title: DOM event listening made easy
tip-number: 50
tip-username: octopitus
tip-username-profile: https://github.com/octopitus
tip-tldr: An elegant and easy way to handle DOM events

categories:
    - en
---
Many of us are still doing these things:

- `element.addEventListener('type', obj.method.bind(obj))`
- `element.addEventListener('type', function (event) {})`
- `element.addEventListener('type', (event) => {})`

Closure keeps a pointer to its enclosing scope. As a result, atttaching a closure to a DOM element can create a circular reference and thus, a memory leak. Since `element` also keeps a reference to the closure, we have a cycle that won't be cleaned up by garbage collection.

Unless you have addressed your handlers in a way you can remove it later on, otherwise you will never able to remove them. And there must be the correct ways:

Use a reference:
```js
const handler = function () {
  console.log("Tada!")
}
element.addEventListener("click", handler)
// Later on
element.removeEventListener("click", handler)
```

Named function that removes itself:
```js
element.addEventListener('click', function click(e) {
  if (someCondition) {
    return e.currentTarget.removeEventListener('click', click);
  }
});
```

A better approach:
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

// Anytime you need
const handleClick = handleEvent('click', {
  onElement: element,
  withCallback: (event) => {
    console.log('Tada!')
  }
})

// And anytime you want to remove it
handleClick.destroy()
```
