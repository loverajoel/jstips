---
layout: post

title: 选择（picking）和反选（rejecting）对象的属性 
tip-number: 70
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: 有时候我们需要将一个对象的某些属性放到白名单里，这样来说，我们有一个数组代表了一张数据库表，并且为了一些功能我们需要从中选出（`select`）一些字段。

categories:
    - zh_CN
    - javascript
---


有时候我们需要将一个对象的某些属性放到白名单里，这样来说，我们有一个数组代表了一张数据库表，并且为了一些功能我们需要从中选出（`select`）一些字段：

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

pick(row, ['client.name']); // 取到了 client name

table.map(row => pick(row, ['client.name'])); // 取到了一系列 client name
```

在 pick 函数中用到了一点‘诡计’。首先，我们用 `map` 遍历了键名数组（keys）, 每次都会返回一个包含当前键名（key）的对象（如果在目标对象（obj）中没有当前键名，就会返回空对象）。然后我们用 `reduce` 把返回的所有单个键-值对象和合并到一个对象中。

但是，如果我们想反选（`reject`）属性／键名呢？改造一下我们的函数就好了：

``` javascript
function reject(obj, keys) {
    return Object.keys(obj)
        .filter(k => !keys.includes(k))
        .map(k => ({[k]: obj[k]}))
        .reduce((res, o) => Object.assign(res, o), {});
}

// 或者, 利用 pick
function reject(obj, keys) {
    const vkeys = Object.keys(obj)
        .filter(k => !keys.includes(k));
    return pick(obj, vkeys);
}

reject({a: 2, b: 3, c: 4}, ['a', 'b']); // => {c: 4}
```