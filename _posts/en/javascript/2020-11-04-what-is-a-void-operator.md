---
layout: post

title: What is a void operator?
tip-number: 79
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: The void operator returns an undefined value from an evaluated expression

categories:
    - en
    - javascript
---
The `void` operator returns an `undefined` value from an evaluated expression, or in other words; the `void` operator specifies an expression to be evaluated without returning a value. It is commonly used in client-side JavaScript, where the browser should not display the value.

```js
function getYear() {
  return 2020;
};

console.log(getYear());
// Output: 2020

console.log(void getYear());
// Output: undefined

// Useful use case
button.onclick = () => void getYear();
```
