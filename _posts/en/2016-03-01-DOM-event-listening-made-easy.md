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

You’ll never be able to remove those listeners. Unless you have addressed your handler in a way you can remove it later on. otherwise you might do is wrong already.

There must be the correct ways:
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

And a better approach:
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
    console.log('Clicked on', target)
  }
})

// And anytime you want to remove it
handleClick.destroy()
```
