---
layout: post

title: Picking and rejecting object properties 
tip-number: 70
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: Sometimes we need to whitelist certain attributes from an object, say we've got an array representation of a database table and we need to `select` just a few fields for some function.

categories:
    - en
    - javascript
---


Sometimes we need to whitelist certain attributes from an object, say we've
got an array representation of a database table and we need to `select` just
a few fields for some function:

``` javascript
function pick(obj, keys) {
    return keys.map(k => k in obj ? {[k]: obj[k]} : {})
               .reduce((res, o) => Object.assign(res, o), {});
}

const row = {
    'accounts.id': 1,
    'client.name': 'John Doe',
    'bank.code': 'MDAKW213'
};

const table = [
    row,
    {'accounts.id': 3, 'client.name': 'Steve Doe', 'bank.code': 'STV12JB'}
];

pick(row, ['client.name']); // Get client name

table.map(row => pick(row, ['client.name'])); // Get a list of client names
```

There's a bit of skulduggery going on in pick. First, we `map` a function over
the keys that will return, each time, an object with only the attribute pointed
by the current key (or an empty object if there's no such attribute in the
object). Then, we `reduce` this collection of single-attribute objects by
merging the objects.

But what if we want to `reject` the attributes? Well, the function changes a bit

``` javascript
function reject(obj, keys) {
    return Object.keys(obj)
        .filter(k => !keys.includes(k))
        .map(k => Object.assign({}, {[k]: obj[k]}))
        .reduce((res, o) => Object.assign(res, o), {});
}

// or, reusing pick
function reject(obj, keys) {
    const vkeys = Object.keys(obj)
        .filter(k => !keys.includes(k));
    return pick(obj, vkeys);
}

reject({a: 2, b: 3, c: 4}, ['a', 'b']); // => {c: 4}
```