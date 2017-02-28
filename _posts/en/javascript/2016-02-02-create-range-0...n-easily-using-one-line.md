---
layout: post

title: Create array sequence `[0, 1, ..., N-1]` in one line
tip-number: 33
tip-username: SarjuHansaliya
tip-username-profile: https://github.com/SarjuHansaliya
tip-tldr: Compact one-liners that generate ordinal sequence arrays

redirect_from:
  - /en/create-range-0...n-easily-using-one-line/

categories:
    - en
    - javascript
---

Here are two compact code sequences to generate the `N`-element array `[0, 1, ..., N-1]`:

### Solution 1 (requires ES5)

```js
Array.apply(null, {length: N}).map(Function.call, Number);
```

#### Brief explanation

1. `Array.apply(null, {length: N})` returns an `N`-element array filled with `undefined` (i.e. `A = [undefined, undefined, ...]`).
2. `A.map(Function.call, Number)` returns an `N`-element array, whose index `I` gets the result of `Function.call.call(Number, undefined, I, A)`
3. `Function.call.call(Number, undefined, I, A)` collapses into `Number(I)`, which is naturally `I`.
4. Result: `[0, 1, ..., N-1]`.

For a more thorough explanation, go [here](https://github.com/gromgit/jstips-xe/blob/master/tips/33.md).

### Solution 2 (requires ES6)
It uses `Array.from` [https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
```js
Array.from(new Array(N),(val,index)=>index);
```

### Solution 3 (requires ES6)

```js
Array.from(Array(N).keys());
```

#### Brief explanation

1. `A = new Array(N)` returns an array with `N` _holes_ (i.e. `A = [,,,...]`, but `A[x] = undefined` for `x` in `0...N-1`).
2. `F = (val,index)=>index` is simply `function F (val, index) { return index; }`
3. `Array.from(A, F)` returns an `N`-element array, whose index `I` gets the results of `F(A[I], I)`, which is simply `I`.
4. Result: `[0, 1, ..., N-1]`.

### One More Thing

If you actually want the sequence [1, 2, ..., N], **Solution 1** becomes:

```js
Array.apply(null, {length: N}).map(function(value, index){
  return index + 1;
});
```

and **Solution 2**:

```js
Array.from(new Array(N),(val,index)=>index+1);
```
