---
layout: post

title: Currying vs partial application
tip-number: 28
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: Currying and partial application are two ways of transforming a function into another function with a generally smaller arity.


redirect_from:
  - /en/curry-vs-partial-application/

categories:
    - en
    - javascript
---

**Currying**

Currying takes a function 

f: X * Y -> R

and turns it into a function

f': X -> (Y -> R)

Instead of calling f with two arguments, we invoke f' with the first argument. The result is a function that we then call with the second argument to produce the result. 

Thus, if the uncurried f is invoked as

f(3,5)

then the curried f' is invoked as

f(3)(5)

For example:
Uncurried add()

```javascript

function add(x, y) {
  return x + y;
}

add(3, 5);   // returns 8
```

Curried add()

```javascript
function addC(x) {
  return function (y) {
    return x + y;
  }
}

addC(3)(5);   // returns 8
```

**The algorithm for currying.** 

Curry takes a binary function and returns a unary function that returns a unary function.

curry: (X × Y → R) → (X → (Y → R))

Javascript Code:

```javascript
function curry(f) {
  return function(x) {
    return function(y) {
      return f(x, y);
    }
  }
}
```

**Partial application**

Partial application takes a function

f: X * Y -> R

and a fixed value for the first argument to produce a new function

f`: Y -> R

f' does the same as f, but only has to fill in the second parameter which is why its arity is one less than the arity of f.

For example: Binding the first argument of function add to 5 produces the function plus5.

```javascript
function plus5(y) {
  return 5 + y;
}

plus5(3);  // returns 8
```

**The algorithm of partial application.*** 

partApply takes a binary function and a value and produces a unary function. 

partApply : ((X × Y → R) × X) → (Y → R)

Javascript Code:

```javascript
function partApply(f, x) {
  return function(y) {
    return f(x, y);
  }
}
```
