---
layout: post

title: Basics declarations
tip-number: 47
tip-username: adaniloff 
tip-username-profile: https://github.com/adaniloff
tip-tldr: Understand and work with declarations.

redirect_from:
  - /en/basics-declarations/

categories:
    - en
    - javascript
---

Below, different ways to declare variables in JavaScript. 
Comments and console.log should be enough to explain what's happening here:

```js
var y, x = y = 1 //== var x; var y; x = y = 1
console.log('--> 1:', `x = ${x}, y = ${y}`)

// Will print
//--> 1: x = 1, y = 1
```

First, we just set two variables. Nothing much here.

```js
;(() => { 
  var x = y = 2 // == var x; x = y = 2;
  console.log('2.0:', `x = ${x}, y = ${y}`)
})()
console.log('--> 2.1:', `x = ${x}, y = ${y}`)

// Will print
//2.0: x = 2, y = 2
//--> 2.1: x = 1, y = 2
```

As you can see, the code has only changed the global y, as we haven't declared the variable in the closure.

```js
;(() => { 
  var x, y = 3 // == var x; var y = 3;
  console.log('3.0:', `x = ${x}, y = ${y}`)
})()
console.log('--> 3.1:', `x = ${x}, y = ${y}`)

// Will print
//3.0: x = undefined, y = 3
//--> 3.1: x = 1, y = 2
```

Now we declare both variables through var. Meaning they only live in the context of the closure.

```js
;(() => { 
  var y, x = y = 4 // == var x; var y; x = y = 4
  console.log('4.0:', `x = ${x}, y = ${y}`)
})()
console.log('--> 4.1:', `x = ${x}, y = ${y}`)

// Will print
//4.0: x = 4, y = 4
//--> 4.1: x = 1, y = 2
```

Both variables have been declared using var and only after that we've set their values. As local > global, x and y are local in the closure, meaning the global x and y are untouched.

```js
x = 5 // == x = 5
console.log('--> 5:', `x = ${x}, y = ${y}`)

// Will print
//--> 5: x = 5, y = 2
```

This last line is explicit by itself.

You can test this and see the result [thanks to babel](https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=var%20y%2C%20x%20%3D%20y%20%3D%201%20%2F%2F%3D%3D%20var%20x%3B%20var%20y%3B%20x%20%3D%20y%20%3D%201%0Aconsole.log('--%3E%201%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%0A%2F%2F%20Will%20print%0A%2F%2F--%3E%201%3A%20x%20%3D%201%2C%20y%20%3D%201%0A%0A%3B(()%20%3D%3E%20%7B%20%0A%20%20var%20x%20%3D%20y%20%3D%202%20%2F%2F%20%3D%3D%20var%20x%3B%20y%20%3D%202%3B%0A%20%20console.log('2.0%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%7D)()%0Aconsole.log('--%3E%202.1%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%0A%2F%2F%20Will%20print%0A%2F%2F2.0%3A%20x%20%3D%202%2C%20y%20%3D%202%0A%2F%2F--%3E%202.1%3A%20x%20%3D%201%2C%20y%20%3D%202%0A%0A%3B(()%20%3D%3E%20%7B%20%0A%20%20var%20x%2C%20y%20%3D%203%20%2F%2F%20%3D%3D%20var%20x%3B%20var%20y%20%3D%203%3B%0A%20%20console.log('3.0%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%7D)()%0Aconsole.log('--%3E%203.1%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%0A%2F%2F%20Will%20print%0A%2F%2F3.0%3A%20x%20%3D%20undefined%2C%20y%20%3D%203%0A%2F%2F--%3E%203.1%3A%20x%20%3D%201%2C%20y%20%3D%202%0A%0A%3B(()%20%3D%3E%20%7B%20%0A%20%20var%20y%2C%20x%20%3D%20y%20%3D%204%20%2F%2F%20%3D%3D%20var%20x%3B%20var%20y%3B%20x%20%3D%20y%20%3D%203%0A%20%20console.log('4.0%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%7D)()%0Aconsole.log('--%3E%204.1%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%0A%2F%2F%20Will%20print%0A%2F%2F4.0%3A%20x%20%3D%204%2C%20y%20%3D%204%0A%2F%2F--%3E%204.1%3A%20x%20%3D%201%2C%20y%20%3D%202%0A%0Ax%20%3D%205%20%2F%2F%20%3D%3D%20x%20%3D%205%0Aconsole.log('--%3E%205%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%0A%2F%2F%20Will%20print%0A%2F%2F--%3E%205%3A%20x%20%3D%205%2C%20y%20%3D%202).

More informations available on the [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var).

Special thanks to @kurtextrem for his collaboration :)!
