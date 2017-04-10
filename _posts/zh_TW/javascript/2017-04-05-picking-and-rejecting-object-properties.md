---
layout: post

title: 選擇或是拋棄物件屬性
tip-number: 70
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: 有時候我們需要列出物件中某些屬性，假設我們有一個陣列來表達一個資料表，我們需要有些 function 來 `select` 欄位。

categories:
    - zh_TW
    - javascript
---


有時候我們需要列出物件中某些屬性，假設我們有一個陣列來表達一個資料表，我們需要有些 function 來 `select` 欄位：

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

pick(row, ['client.name']); // 取得 Client 名稱

table.map(row => pick(row, ['client.name'])); // 取得一些 client 名稱的列表
```

在 pick 我們透過一個小手段，首先，我們 `map` 一個 function，每次透過目前的 key 只有該屬性的物件被回傳（或者，如果在物件內沒有任何的屬性會回傳一個空的物件）。然後透過 merge 物件，我們 `reduce` 這些單一屬性的集合物件。

但是如果我們想要 `reject` 屬性呢？好吧，function 需要一些改變：

``` javascript
function reject(obj, keys) {
    return Object.keys(obj)
        .filter(k => !keys.includes(k))
        .map(k => Object.assign({}, {[k]: obj[k]}))
        .reduce((res, o) => Object.assign(res, o), {});
}

// 或者恢復 pick
function reject(obj, keys) {
    const vkeys = Object.keys(obj)
        .filter(k => !keys.includes(k));
    return pick(obj, vkeys);
}

reject({a: 2, b: 3, c: 4}, ['a', 'b']); // => {c: 4}
```
