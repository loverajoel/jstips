---
layout: post

title: What is the difference between Target and currentTarget in the event context?
tip-number: 77
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: Temporal Dead Zone is a JavaScript behavior while using variables declared using `let` and `const` keywords.

categories:
    - en
    - javascript
---
`target` refers to the DOM element that triggers an event. Otherwise, `currentTarget` refers to the DOM element that the event listener is listening on.

```html
<ul class="todo-list">
  <li class="item">Walk your dog</li>
</ul>
```

```js
const list = document.querySelector(".todo-list");

list.addEventListener("click", e => {
  console.log(e.target);
  // Output: <li class="item">Walk your dog</li>
  console.log(e.currentTarget);
  // Output: <ul class="todo-list"></ul>
});
```