---
layout: post

title: Protocols for the Brave 
tip-number: 73
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: You might have heard about the old ways gaining hype recently, and we don't mean praying to the gods of the north. Today we're introducing a feature found in Clojure which allows you to define interfaces for your classes.

categories:
    - en
    - javascript
---


You might have heard about the old ways gaining hype recently, and we don't
mean praying to the gods of the north.

Functional programming is the rediscovered toy which is bringing some sanity
to the world of mutable state and global bindings.

Today we're introducing a feature found in Clojure which allows you to define
interfaces for your classes. Let's look at one-off implementation:

``` javascript
const protocols = (...ps) => ps.reduce((c, p) => p(c), Object);

const Mappable = (klass) => {
    return class extends klass {
        map() {
            throw 'Not implemented';
        }
    };
};

const Foldable = (klass) => {
    return class extends klass {
        fold() {
            throw 'Not implemented';
        }
    };
};

class NaturalNumbers extends protocols(Mappable, Foldable) {
    constructor() {
        super();
        this.elements = [1,2,3,4,5,6,7,8,9];
    }

    map (f) {
        return this.elements.map(f);
    }

    fold (f) {
        return this.elements.reduce(f, this.elements, 0);
    }
}
```

Yes, we're building a chain of class inheritance up there with that reduce boy.
It's pretty cool. We're doing it dynamically! You see, each protocol receives
a base class (Object) and extends it somehow returning the new class. The idea
is similar to that of interfaces.

We supply method signatures for the protocol and make sure we provide
implementations for it on our base classes.

What's so cool about it? We get to write things like these:

``` javascript
const map = f => o => o.map(f);
const fold = f => o => o.fold(f);
const compose = (... fns) => fns.reduce((acc, f) => (x) => acc(f(x)), id);
```

Ok, maybe we could have written those two functions without the above fuzz but,
now that we know `NaturalNumbers` are `Mappable`, we can call `map` on them
and trust it will return the right result. Furthermore, with our third function,
we can *compose* any number of operations defined in protocols cleanly:

``` javascript
const plus1 = x => x + 1;
const div5 = x => x / 5;
const plus_then_div = compose(map(div5), map(plus1));
console.log(plus_then_div(new NaturalNumbers));
// => [ 0.4, 0.6, 0.8, 1, 1.2, 1.4, 1.6, 1.8, 2 ]
```

More important, if we know that an object of ours is `Mappable`, we know `map`
will work on it. Protocols gives us an idea of what we can do with an object and
help us abstract common operations between data types, thus reducing the
overhead of dealing with a hundred functions.

What is easier? To have a hundred functions for every different object or  ten
functions that work on a hundred objects?