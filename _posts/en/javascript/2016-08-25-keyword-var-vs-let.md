---
layout: post

title: ES6, var vs let
tip-number: 59
tip-username: richzw
tip-username-profile: https://github.com/richzw
tip-tldr: In this tip, I will introduce the block-scope difference between keyword var and let. Should I replace var by let? let's take a look


redirect_from:
  - /en/keyword-var-vs-let/

categories:
    - en
    - javascript
---

### Overview

- The scope of a variable defined with `var` is function scope or declared outside any function, global.
- The scope of a variable defined with `let` is block scope.

```js
function varvslet() {
  console.log(i); // i is undefined due to hoisting
  // console.log(j); // ReferenceError: j is not defined

  for( var i = 0; i < 3; i++ ) {
    console.log(i); // 0, 1, 2
  };

  console.log(i); // 3
  // console.log(j); // ReferenceError: j is not defined

  for( let j = 0; j < 3; j++ ) {
    console.log(j);
  };

  console.log(i); // 3
  // console.log(j); // ReferenceError: j is not defined
}
```

### Difference Details

- Variable Hoisting

  `let` will not hoist to the entire scope of the block they appear in. By contrast, `var` could hoist as below.

```js
{
  console.log(c); // undefined. Due to hoisting
  var c = 2;
}

{
  console.log(b); // ReferenceError: b is not defined
  let b = 3;
}
```

- Closure in Loop

  `let` in the loop can re-binds it to each iteration of the loop, making sure to re-assign it the value from the end of the previous loop iteration, so it can be used to avoid issue with closures.

```js
for (var i = 0; i < 5; ++i) {
  setTimeout(function () {
    console.log(i); // output '5' 5 times
  }, 100);  
}
```

  After replacing `var` with `let`
  
```js
// print 1, 2, 3, 4, 5
for (let i = 0; i < 5; ++i) {
  setTimeout(function () {
    console.log(i); // output 0, 1, 2, 3, 4 
  }, 100);  
}
```


### Should I replace `var` with `let`?

> NO, `let` is the new block scoping `var`. That statement emphasizes that `let` should replace `var` only when `var` was already signaling
block scoping stylistically. Otherwise, leave `var` alone. `let` improves scoping options in JS, not replaces. `var` is still a useful signal for variables that are used throughout the function. 

### `let` compatibility

- In server side, such as Node.js, you can safely use the `let` statement now.
  
- In client side, through a transpiler (like [Traceur](https://github.com/google/traceur-compiler)), you can safely use the `let` statement. Otherwise, please consider the browser support [here](http://caniuse.com/#search=let)

### Playground
<div>
  <a class="jsbin-embed" href="http://jsbin.com/yumaye/embed?js,console">JS Bin on jsbin.com</a><script src="http://static.jsbin.com/js/embed.min.js?3.39.11"></script>
</div>

### More info

- [Let keyword vs var keyword](http://stackoverflow.com/questions/762011/let-keyword-vs-var-keyword)
- [For and against let](https://davidwalsh.name/for-and-against-let)
- [Explanation of `let` and block scoping with for loops](http://stackoverflow.com/questions/30899612/explanation-of-let-and-block-scoping-with-for-loops/30900289#30900289).