---
layout: post

title: 進階 JavaScript 屬性
tip-number: 39
tip-username: mallowigi
tip-username-profile: https://github.com/mallowigi
tip-tldr: 如何加入私有屬性、getters 和 setters 到物件。


redirect_from:
  - /zh_tw/advanced-properties/

categories:
    - zh_TW
    - javascript
---

在 JavaScript 可以設定物件屬性，例如：將屬性設定成偽私有或是唯讀。這是 ECMAScript 5.1 可用的功能，因此支援所有現代的瀏覽器。

如果需要這麼做，你需要使用 `Object` 的 `defineProperty` 方法，像是：

```js
var a = {};
Object.defineProperty(a, 'readonly', {
  value: 15,
  writable: false
});

a.readonly = 20;
console.log(a.readonly); // 15
```

語法如下：
```js
Object.defineProperty(dest, propName, options)
```

或是多個定義：
```js
Object.defineProperties(dest, {
  propA: optionsA,
  propB: optionsB, //...
})
```

其中，包括以下可選的屬性：
- *value*：如果屬性不是 getter（如下），數值是必要的屬性。`{a: 12}` === `Object.defineProperty(obj, 'a', {value: 12})`
- *writable*：將屬性設定為唯讀。請注意，如果該屬性是巢狀的物件，該屬性是仍然可以編輯。
- *enumerable*：將屬性設定為隱藏。這意思說，在 `for ... of` 迴圈和 `stringify` 的結果不包含屬性，但屬性仍然存在。注意：這不代表屬性為私有的！它依然可以從外部存取，它只是不會列印出來。
- *configurable*：將屬性設定為不可修改。防止刪除或重新定義。再者，如果該屬性是一個巢狀的物件，其屬性仍然可以設定。


因此，為了建立一個私有的常數屬性，你像可以這樣定義：

```js
Object.defineProperty(obj, 'myPrivateProp', {value: val, enumerable: false, writable: false, configurable: false});
```

除了設定屬性，由於第二個參數是一個字串，`defineProperty` 允許我們定義*動態屬性*。舉個例子，比如說我想要根據一些外部設定來建立屬性：

```js

var obj = {
  getTypeFromExternal(): true // 違反 ES5.1 規則
}

Object.defineProperty(obj, getTypeFromExternal(), {value: true}); // ok

// 因為範例緣故， ES6 引入了一個新語法：
var obj = {
  [getTypeFromExternal()]: true
}
```

但是這還不是全部！進階屬性允許我們建立 **getters** 和 **setters**，就像其他物件導向語言一樣！在這個情況下，我們不能使用 `writable`、`enumerable` 和 `configurable` 屬性，而是：

```js
function Foobar () {
  var _foo; //  true 私有屬性

  Object.defineProperty(obj, 'foo', {
    get: function () { return _foo; }
    set: function (value) { _foo = value }
  });

}

var foobar = new Foobar();
foobar.foo; // 15
foobar.foo = 20; // _foo = 20
```

除了有明顯的封裝和存取的優點，你可以注意到我們沒有「呼叫」getter，相反的，我們只是「取得」不帶括號的屬性！這太棒了！舉個例子，讓我們想像我們有一個物件具有多層巢狀的屬性，像是：

```js
var obj = {a: {b: {c: [{d: 10}, {d: 20}] } } };
```

現在我們不需要做 `a.b.c[0].d`（其中某個屬性可以解析成 `undefined` 然後拋出錯誤），我們可以建立另一個別名：

```js
Object.defineProperty(obj, 'firstD', {
  get: function () { return a && a.b && a.b.c && a.b.c[0] && a.b.c[0].d }
})

console.log(obj.firstD) // 10
```

### 注意
如果你定義一個 getter 而沒有一個 setter 然後你想要嘗試設定數值，你會得到一個錯誤！當使用輔助函式像是 `$.extend` 或 `_.merge`，這是相當重要的一部份。請小心使用！

### 連結

- [defineProperty](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)
- [在 JavaScript 中定義屬性](http://bdadam.com/blog/defining-properties-in-javascript.html)
