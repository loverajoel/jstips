---
layout: post

title: DOM event listening made easy
tip-number: 51
tip-username: octopitus
tip-username-profile: https://github.com/octopitus
tip-tldr: An elegant and easy way to handle DOM events

redirect_from:
  - /en/DOM-event-listening-made-easy/

categories:
    - en
    - javascript
---
Many of us are still doing these things:

- `element.addEventListener('type', obj.method.bind(obj))`
- `element.addEventListener('type', function (event) {})`
- `element.addEventListener('type', (event) => {})`

The above examples all create new anonymous event handlers that can't be removed when no longer needed. This may cause performance problems or unexpected logic bugs, when handlers that you no longer need still get accidentally triggered through unexpected user interactions or [event bubbling](http://www.javascripter.net/faq/eventbubbling.htm).

Safer event-handling patterns include the following:

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
