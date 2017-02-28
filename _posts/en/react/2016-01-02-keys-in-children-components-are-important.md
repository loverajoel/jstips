---
layout: post

title: Keys in children components are important
tip-number: 02
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: The key is an attribute that you must pass to all components created dynamically from an array. It's a unique and constant id that React uses to identify each component in the DOM and to know whether it's a different component or the same one. Using keys ensures that the child component is preserved and not recreated and prevents weird things from happening.
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /en/keys-in-children-components-are-important/

categories:
    - en
    - react
---

The [key](https://facebook.github.io/react/docs/multiple-components.html#dynamic-children) is an attribute that you must pass to all components created dynamically from an array. It's a unique and constant id that React uses to identify each component in the DOM and to know whether it's a different component or the same one. Using keys ensures that the child component is preserved and not recreated and prevents weird things from happening.

> Key is not really about performance, it's more about identity (which in turn leads to better performance). Randomly assigned and changing values do not form an identity [Paul O’Shannessy](https://github.com/facebook/react/issues/1342#issuecomment-39230939)

- Use an existing unique value of the object.
- Define the keys in the parent components, not in child components

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
- [Using array index is a bad practice.](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318#.76co046o9)
- `random()` will not work

```javascript
//bad
<MyComponent key={% raw %}{{Math.random()}}{% endraw %}/>
```

- You can create your own unique id. Be sure that the method is fast and attach it to your object.
- When the number of children is large or contains expensive components, use keys to improve performance.
- [You must provide the key attribute for all children of ReactCSSTransitionGroup.](http://docs.reactjs-china.com/react/docs/animation.html)