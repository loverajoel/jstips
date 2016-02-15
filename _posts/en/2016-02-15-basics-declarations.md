---
layout: post

title: Basics declarations
tip-number: 47
tip-username: adaniloff 
tip-username-profile: https://github.com/adaniloff
tip-tldr: Understand and work with declarations.

categories:
    - en
---

Below, different ways to declare variables in javascript.
Comments and console.log should be enough to explain what's happening here:

```js
var y, x = y = 1 //== var x; var y; x = y = 1
console.log('--> 1:', `x = ${x}, y = ${y}`)

// Will print
//--> 1: x = 1, y = 1

;(() => { 
  var x = y = 2 // == var x; y = 2;
  console.log('2.0:', `x = ${x}, y = ${y}`)
})()
console.log('--> 2.1:', `x = ${x}, y = ${y}`)

// Will print
//2.0: x = 2, y = 2
//--> 2.1: x = 1, y = 2

;(() => { 
  var x, y = 3 // == var x; var y = 3;
  console.log('3.0:', `x = ${x}, y = ${y}`)
})()
console.log('--> 3.1:', `x = ${x}, y = ${y}`)

// Will print
//3.0: x = undefined, y = 3
//--> 3.1: x = 1, y = 2

;(() => { 
  var y, x = y = 4 // == var x; var y; x = y = 3
  console.log('4.0:', `x = ${x}, y = ${y}`)
})()
console.log('--> 4.1:', `x = ${x}, y = ${y}`)

// Will print
//4.0: x = 4, y = 4
//--> 4.1: x = 1, y = 2

x = 5 // == x = 5
console.log('--> 5:', `x = ${x}, y = ${y}`)

// Will print
//--> 5: x = 5, y = 2
```

More informations available on the [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var).

