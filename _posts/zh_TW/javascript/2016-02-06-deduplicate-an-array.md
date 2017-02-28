---
layout: post

title: 移除陣列重複元素
tip-number: 37
tip-username: danillouz
tip-username-profile: https://www.twitter.com/danillouz
tip-tldr: 如何從陣列中移除不同資料類型重複的元素。


redirect_from:
  - /zh_tw/deduplicate-an-array/

categories:
    - zh_TW
    - javascript
---

# 原始函數
如果陣列只有包含原始數值，我們可以透過 [`filter`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) 和 [`indexOf`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf) 方法來刪除重複的元素。

```javascript
var deduped = [ 1, 1, 'a', 'a' ].filter(function (el, i, arr) {
	return arr.indexOf(el) === i;
});

console.log(deduped); // [ 1, 'a' ]
```

## ES2015
我們可以使用[箭頭函式](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions)來撰寫讓程式更簡潔。

```javascript
var deduped = [ 1, 1, 'a', 'a' ].filter( (el, i, arr) => arr.indexOf(el) === i);

console.log(deduped); // [ 1, 'a' ]
```

但是根據 [Sets](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set) 和 [`from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) 方法，我們可以用更簡潔的方式得到同樣的結果。

```javascript
var deduped = Array.from( new Set([ 1, 1, 'a', 'a' ]) );

console.log(deduped); // [ 1, 'a' ]
```

# 物件
當元素都是物件時，我們不能使用相同的方法，因為物件儲存的值是參考原始儲存的值。

```javascript
1 === 1 // true

'a' === 'a' // true

{ a: 1 } === { a: 1 } // false
```

因此，我們需要改變我們的方式以及使用雜湊表。

```javascript
function dedup(arr) {
	var hashTable = {};

	return arr.filter(function (el) {
		var key = JSON.stringify(el);
		var match = Boolean(hashTable[key]);

		return (match ? false : hashTable[key] = true);
	});
}

var deduped = dedup([
	{ a: 1 },
	{ a: 1 },
	[ 1, 2 ],
	[ 1, 2 ]
]);

console.log(deduped); // [ {a: 1}, [1, 2] ]
```

因為在 JavaScript 雜湊表只是一個 `Object`，它的 key 的類型是 `String`。意思說，在同一個數值下，我們不能區分字串和數字，例如：`1` 和 `'1'`。

```javascript
var hashTable = {};

hashTable[1] = true;
hashTable['1'] = true;

console.log(hashTable); // { '1': true }
```

然而，因為我們使用了 [`JSON.stringify`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify), keys 是 `String` 的類型，會被轉成字串儲存，這樣 `hashTable` key 就是唯一的。

```javascript
var hashTable = {};

hashTable[JSON.stringify(1)] = true;
hashTable[JSON.stringify('1')] = true;

console.log(hashTable); // { '1': true, '\'1\'': true }
```

意思說重複相同的元素數值，但為不同類型的，可以被保留，而重複的元素仍然會被刪除。

```javascript
var deduped = dedup([
	{ a: 1 },
	{ a: 1 },
	[ 1, 2 ],
	[ 1, 2 ],
	1,
	1,
	'1',
	'1'
]);

console.log(deduped); // [ {a: 1}, [1, 2], 1, '1' ]
```

# 資源
## 方法
* [`filter`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
* [`indexOf`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)
* [`from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
* [`JSON.stringify`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)

## ES2015
* [箭頭函式](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
* [Sets](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)

## Stack overflow
* [將陣列重複的元素移除](http://stackoverflow.com/questions/9229645/remove-duplicates-from-javascript-array/9229821#9229821)
