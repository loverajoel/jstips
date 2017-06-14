---
layout: post

title: Immutable structures and cloning
tip-number: 78
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: Object cloning is a tricky, full of edge-cases, endeavor. The reason is simple enough. Objects maintain internal state, and that is much abused. There are countless techniques, or better phrased, countless derivations of the same technique.

categories:
    - en
    - javascript
---

Object cloning is a tricky, full of edge-cases, endeavor. The reason is simple
enough. Objects maintain internal state, and that is much abused. There are
countless techniques, or better phrased, countless derivations of the same
technique.

Cloning an object is an indicator that your application is growing, and that
you've got a complex object which you'd want to treat as an immutable value, i.e
operate on it while maintaining a previous state.

If the object is in your control, you're lucky. A bit of refactoring here and
there might lead you to a point where you avoid the problem entirely by
rethinking your object's structure and behavior.

With the rediscovering of functional programming techniques, a myriad of debates
have been held about immutable structures and how they offer exactly what you
seek for. Mutable state is the root of all evil, some might argue.

We encourage to reach **ImmutableJS** by Facebook which provides a nice set of
immutable structures free for use. By rethinking your object's inner workings
and separating state from behavior, making each function consume a state to
produce a new one - much like the Haskell's **State** monad - you will
reduce many nuisances.

If the object is outside your control, you're partly out of luck. This can be
circumvented by creating convoluted computations where you solve for yourself
circular references and reach enlightenment. However, as you're using external
objects anyways, and they must come, as their name says, from external sources,
then you might be more comfortable handling the matter to yet another external
library and focus on what matters the most, i.e, your application itself.

One such library is [pvorb/clone](https://github.com/pvorb/clone), which has a
very simple API. To clone an object you only have to

``` javascript
var clone = require('clone');

var a = {foo: {bar: 'baz'}};
var b = clone(a);
a.foo.bar = 'foo';
console.log(a); // {foo: {bar: 'foo'}}
console.log(b); // {foo: {bar: 'baz'}}
```

There are, of course, many more libraries that allow you to do the same such as
[Ramda](http://ramdajs.com/docs/#clone), [lodash.clonedeep](https://www.npmjs.com/package/lodash.clonedeep)
and [lodash.clone](https://www.npmjs.com/package/lodash.clone).

As an end note, if you are serious about dealing with immutable structures, you
might want to check **ClojureScript** or (for those that feel that Haskell's
worth a shot) **PureScript**.

We neither encourage, nor condemn, the use of self made cloning mechanisms. Only
noting that considerable work has been done on the area and that you'd probably
be better of reusing than reinventing the wheel.