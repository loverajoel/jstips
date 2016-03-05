---
layout: post

title: Create array sequence [0, 1, ..., N-1] in one line
tip-number: 33
tip-username: SarjuHansaliya
tip-username-profile: https://github.com/SarjuHansaliya
tip-tldr: Compact one-liners that generate ordinal sequence arrays


categories:
    - en
---

Here are two compact code sequences to generate the N-element array [0, 1, ..., N-1]:

### Solution 1 (requires ES5)
```js
Array.apply(null, {length: N}).map(Function.call, Number);
```
### Solution 2 (requires ES6)
```js
Array.from(new Array(N),(val,index)=>index);
```

Even a novice developer should be able to explain Solution 2 with a good ES6 reference text, or perhaps [the standards document](http://www.ecma-international.org/ecma-262/6.0/), but Solution 1 is classic [**_High Magic_**](https://en.wikipedia.org/wiki/Ceremonial_magic). It fuses familiar objects and methods in strange combinations, and you get the impression that if you deviate from this incantion by just the tiniest bit, the world will end in a nuclear fireball. You therefore use it _Precisely As Written_, and pray that you're never asked to explain it, or fix it if it fails.

But there's no reason to invoke the Elder Gods, when we can pull back the magic curtain and understand...

### Solution 1: How It Works

##### Step 1: The Unbearable Lightness of `{length: 3}`

We begin with a simple object, `{length: 3}`. It's not an array:
```js
   Object.prototype.toString.call([1,2,3])
=> "[object Array]"
   Object.prototype.toString.call({length: 3})
=> "[object Object]"
```
but it _is_ an **array-like object**: it has a numeric `length` property, and we can access it with the relevant numeric indexes:
```js
   a = {length: 3}   // -> Object {length: 3}
   a[0]              // -> undefined
   a[1]              // -> undefined
   a[2]              // -> undefined
```
(Those `undefined`s are actually irrelevant; all that's important here is that JS returned a value even when you tried to access a non-existent "index".)

##### Step 2: You say `.apply()`, I say `this=null`, let's `.call()` the whole thing off

This comes in handy because, starting with [ES5](https://es5.github.io/multi.html), `Array.apply()` [accepts array-like objects and gets its `length` property](https://es5.github.io/x15.3.html#x15.3.4.3) to iterate over the contents of that object, in a classic `for (i = 0; i < args_obj.length; i++)` loop.

Since the internal algorithms for [`.call()`](https://es5.github.io/x15.3.html#x15.3.4.4) and [`.apply()`](https://es5.github.io/x15.3.html#x15.3.4.3) differ only in how the arguments are treated, we can declare the following:
```js
   X.apply(obj, arr                )
=> X.call (obj, arr[0], arr[1], ...)
=> X      (     arr[0], arr[1], ...) // this = obj
```
which resolves our second step into an [`Array` constructor call](https://es5.github.io/x15.4.html#x15.4.1) as follows:
```js
   b = Array.apply(null, a                                                )
=> b = Array.call (null, undefined(a[0]), undefined(a[1]), undefined(a[2]))
=> b = Array      (      undefined,       undefined,       undefined      )   // this = null
=> b =                  [undefined,       undefined,       undefined      ]
```
We can verify that it's a proper array, and that it supports `.map()` for our next step:
```js
Object.prototype.toString.call(b)  // -> "[object Array]"
Object.keys(b)                     // -> ["0", "1", "2"]
b.length                           // -> 3
b.map                              // -> function map() { [native code] }
```

##### Step 3: You idiot! You forgot to `Number` the bloody `.map()`s!

The logic of `b.map(fn, obj)` is essentially as follows (see [this polyfill implementation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map#Polyfill) for the gory details):
```js
  result = new Array(b.length);
  for (var i = 0; i < b.length; i++) {
    result[i] = fn.call(obj, b[i], i, b);
  }
  return result;
```
But that means `.map(Function.call, Number)` iterates over the following:
```js
   Function.call.call(Number, b[i], i, b)
=> Function.call     (        b[i], i, b)  // this = Number
=> Number            (              i, b)  // this = b[i]
=>                                  i      // Number(x, ...) = x as a number
```
(At this point, I'll replace the definition of `b` with a slightly different 3-element array:
```js
   b = ["Tom", "Dick", "Harry"]
```
I promise that it won't affect the end result; it'll just make the next illustration much clearer.)

So `b.map(Function.call, Number)` resolves as follows:
```js
   ["Tom", "Dick", "Harry"].map(Function.call, Number)

=> [
      Function.call.call(Number, "Tom",   0, ["Tom", "Dick", "Harry"]),
      Function.call.call(Number, "Dick",  1, ["Tom", "Dick", "Harry"]),
      Function.call.call(Number, "Harry", 2, ["Tom", "Dick", "Harry"])
   ]

=> [
      Function.call     (        "Tom",   0, ["Tom", "Dick", "Harry"]),  // this = Number
      Function.call     (        "Dick",  1, ["Tom", "Dick", "Harry"]),  // this = Number
      Function.call     (        "Harry", 2, ["Tom", "Dick", "Harry"])   // this = Number
   ]

=> [
      Number            (                 0, ["Tom", "Dick", "Harry"]),  // this = "Tom"
      Number            (                 1, ["Tom", "Dick", "Harry"]),  // this = "Dick"
      Number            (                 2, ["Tom", "Dick", "Harry"])   // this = "Harry"
   ]

=> [
                                          0,
                                          1,
                                          2
   ]
```

QED.

### Q: So how rigid is Solution 1, really?

Not very. It's true that _most_ of `Array.apply(null, {length: N}).map(Function.call, Number)` needs to be exactly as stated, but there are two terms that are actually quite flexible:

**`null`**: Notice that `this = null` appears too late in the resolution process to be of any use, so you could safely substitute literally _any JS entity_.

**`Function.call`**: This can be replaced with any `X.call` that inherits from `Function.call`. In fact, almost everyone traditionally writes the expression as:
```js
Array.apply(null, {length: N}).map(Number.call, Number)
```
as if `Number.call` needed to be paired with `Number` for the expression to evaluate correctly. The _real_ "magic" is simply that `Number.call` inherits from `Function.call`, nothing more.

This means that all the following expressions return _exactly the same result_ as the main expression:
```js
   function h() {
     console.log("Hello, world!");
   }

   Array.apply(document,               {length: 3}).map(SyntaxError.call, Number)
=> [0, 1, 2]

   Array.apply(234,                    {length: 3}).map(Object.call,      Number)
=> [0, 1, 2]

   Array.apply(new Date("2040-01-01"), {length: 3}).map(h.call,           Number)
=> [0, 1, 2]
   // NOTE: "Hello, world!" was NOT printed, which is to be expected given the resolution process in Step 3.
```

### Oh, and one more thing...

If you want to generate [1, 2, ..., N] instead, you'd have to go with a more conventional `.map()` one-liner:
```js
Array.apply(null, {length: N}).map(function(value, index){ return index+1; });
```
