---
layout: *post

title: DOM event listening made easy
tip-number: 50
tip-username: octopitus
tip-username-profile: https://github.com/octopitus
tip-tldr: Do you believe many of us are doing it wrong?

categories:
    - en
---

Unless you have addressed your handler in a way you can remove it later on, otherwise you might do is wrong already (arrow function, binding, anonymous function,...).

```js
function match (element, selector) {
  const html = document.documentElement
  const matchesSelector = html.matchesSelector || html.webkitMatchesSelector || html.msMatchesSelector || html.mozMatchesSelector
  return matchesSelector.call(element, selector)
}

function elementMatchesSelector (element, selector) {
  if (element && element.nodeType === 1) {
    return match(element, selector)
  }
}

function findClosestElementFromNode (node, {matchingSelector} = {}) {
  while (node && node.nodeType !== Node.ELEMENT_NODE) {
    node = node.parentNode
  }
  if (matchingSelector) {
    while (node) {
      if (elementMatchesSelector(node, matchingSelector)) {
        return node
      }
      node = node.parentNode
    }
  }
  return node
}

function handleEvent (eventName, {onElement, matchingSelector, withCallback, useCapture = false, times} = {}) {
  const element = onElement || document.documentElement

  function handler (event) {
    if (times && --times === 0) {
      handler.destroy()
    }
    const target = findClosestElementFromNode(event.target, {matchingSelector})
    if (!matchingSelector || target) {
      if (typeof withCallback === 'function') {
        withCallback.call(null, event, target)
      }
    }
  }

  handler.destroy = function () {
    return element.removeEventListener(eventName, handler, useCapture)
  }

  element.addEventListener(eventName, handler, useCapture)
  return handler
}
```

And somewhere in your application:

```js
const element = document.getElementById('id')

// Anytime you need
// Handle 'click' on #id
const handleClick = handleEvent('click', {
  onElement: element,
  matchSelector: '.foo',
  withCallback: (event, target) => {
    // Only get called when click on .foo inside element
    // Good for event delegation
    console.log('Clicked on', target)
  }
})

// And anytime you want to remove it
handleClick.destroy()

// Handle 'click' only one time
const handleClick = handleEvent('click', {
  times: 1,
  onElement: element,
  withCallback: (event, target) => {
    console.log('Clicked on', target)
  }
})
```
