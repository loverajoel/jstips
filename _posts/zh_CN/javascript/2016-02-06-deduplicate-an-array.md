---
layout: post

title: 数组去重
tip-number: 37
tip-username: danillouz
tip-username-profile: https://www.twitter.com/danillouz
tip-tldr: 移除包含不同类型数据的数组中重复的元素。


redirect_from:
  - /zh_cn/deduplicate-an-array/

categories:
    - zh_CN
    - javascript
---

# 原始变量
如果一个数组只包含原始变量，我们可以使用[`filter`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)和[`indexOf`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)方法将其去重：

```javascript
var deduped = [ 1, 1, 'a', 'a' ].filter(function (el, i, arr) {
	return arr.indexOf(el) === i;
});

console.log(deduped); // [ 1, 'a' ]
```

## ES2015
我们可以使用[箭头函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)使写法更简明：

```javascript
var deduped = [ 1, 1, 'a', 'a' ].filter( (el, i, arr) => arr.indexOf(el) === i);

console.log(deduped); // [ 1, 'a' ]
```

但是根据[Sets](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set)和[`from`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/from)方法的介绍，我们可以更简明的实现。

```javascript
var deduped = Array.from( new Set([ 1, 1, 'a', 'a' ]) );

console.log(deduped); // [ 1, 'a' ]
```

# Objects
当元素为对象(Object)时，我们就不能用这种办法了，
因为对象存储的是引用而原始变量存储的是值。

```javascript
1 === 1 // true

'a' === 'a' // true

{ a: 1 } === { a: 1 } // false
```

因此我们需要改变一下我们的实现方法，使用哈希表。

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

因为哈希表在Javascript里是一个简单的`Object`，它的`key`永远是`String`类型。这意味着我们不能区分字符串和数字表示的相同的值，如`1`和`'1'`。

```javascript
var hashTable = {};

hashTable[1] = true;
hashTable['1'] = true;

console.log(hashTable); // { '1': true }
```

然而，因为我们使用的[`JSON.stringify`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)，`String`类型的`key`
将会被存储为一个字符串值，这样`hashTable`的`key`就唯一了。

```javascript
var hashTable = {};

hashTable[JSON.stringify(1)] = true;
hashTable[JSON.stringify('1')] = true;

console.log(hashTable); // { '1': true, '\'1\'': true }
```

这意味着相同的值，但不同类型的元素，将以原来的格式保留。

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

# 阅读材料
## 函数
* [`filter`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
* [`indexOf`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)
* [`from`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
* [`JSON.stringify`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)

## ES2015
* [箭头函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
* [Set](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set)

## Stack overflow
* [remove duplicates from array](http://stackoverflow.com/questions/9229645/remove-duplicates-from-javascript-array/9229821#9229821)
