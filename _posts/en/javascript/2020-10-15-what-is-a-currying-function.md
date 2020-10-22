---
layout: post

title: What is a currying function?
tip-number: 75
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: A currying function is a function that takes multiple arguments and turns it into a sequence of functions having only one argument at a time.

categories:
    - en
    - javascript
---

A currying function is a function that takes multiple arguments and turns it into a sequence of functions having only one argument at a time.

In this way, an n-ary function becomes a unary function, and the last function returns the result of all the arguments together in a function.


```javascript
// Normal definition
function multiply(a, b, c) {
    return a * b * c;
};
console.log(multiply(1, 2, 3));
// Output: 6

// Simple curry function definition
function multiply(a) {
    return (b) => {
        return (c) => {
            return a * b * c;
        };
    };
};
console.log(multiply(1)(2)(3));
// Output: 6
```

### Further readings:

- [Currying in JavaScript](https://dev.to/suprabhasupi/currying-in-javascript-1k3l)
- [Lodash curry](https://lodash.com/docs/#curry)
- [JavaScript currying](http://zetcode.com/javascript/currying/)
