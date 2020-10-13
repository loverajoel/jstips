---
layout: post

title: Closures inside loops
tip-number: 76
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: Closure in a loop is an interesting topic and this is the tip to be a master of it

categories:
    - en
    - javascript
---

If you ever come across the likes of

```javascript
var funcs = [];
for (var i = 0; i < 3; i++) {
  funcs[i] = function() {
    console.log("i value is " + i);
  };
}

for (var k = 0; k < 3; k++) {
  funcs[k]();
}
```

You will notice that the expected output of

```
i value is 0
i value is 1
i value is 2
```

Doesn't match the actual output which will resemble

```
i value is 3
i value is 3
i value is 3
```

This is because of how the capturing mechanism of closures work and how `i` is represented internally.

To solve this situation you can do as follows:

```javascript
for (var i = 0; i < 3; i++) {
  funcs[i] = (function(value) {
    console.log("i value is " + i);
  })(i);
}
```

Which effectively copies i by value by handing it to our closure or

```javascript
for (let i = 0; i < 3; i++) {
  funcs[i] = function() {
    console.log("i value is " + i);
  }
}
```

Where `let` scopes the variable to our `for` loop and produces a new value each iteration, thus `i` will be bound to different values on our closures as expected.
