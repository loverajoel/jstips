---
layout: post

title: 實作非同步迴圈
tip-number: 34
tip-username: madmantalking
tip-username-profile: https://github.com/madmantalking
tip-tldr: 你或許可以實作非同步迴圈，但是執行時可能會遇到問題。

redirect_from:
  - /zh_tw/implementing-asynchronous-loops/

categories:
    - zh_TW
    - javascript
---

讓我們嘗試撰寫一個非同步的函式，在每秒列印出迴圈的索引值。

```js
for (var i = 0; i < 5; i++) {
	setTimeout(function(){
		console.log(i);
	}, 1000 * (i + 1));
}
```
上面的程式將會輸出以下的結果：

```js
> 5
> 5
> 5
> 5
> 5
```
所以這肯定是不能執行的。

**原因**

每個 timeout 指向到原來的 `i`，而非拷貝的。所以在迴圈下 `i` 會增加直到 5，然後 timeout 執行並使用目前的 `i` 數值（i 是 5）。

當然，這個問題看似簡單。一個直接的解決方法就是將迴圈的索引暫存到變數。

```js
for (var i = 0; i < 5; i++) {
	var temp = i;
 	setTimeout(function(){
		console.log(temp);
	}, 1000 * (i + 1));
}
```
但以上的程式輸出的結果是：

```js
> 4
> 4
> 4
> 4
> 4
```

所以，一樣不能執行，因為區塊初始化時沒有建立一個範圍和變數，把它們提升到 scope 的頂部。事實上，在前面的程式碼也是相同的：

```js
var temp;
for (var i = 0; i < 5; i++) {
 	temp = i;
	setTimeout(function(){
		console.log(temp);
  	}, 1000 * (i + 1));
}
```
**解決辦法**

這裡有一些不同的方式來複製 `i`。一般的方式是建立一個 closure，宣告一個函式並將 `i` 作為一個參數傳送。在這裡我們做了一個立即函式。

```js
for (var i = 0; i < 5; i++) {
	(function(num){
		setTimeout(function(){
			console.log(num);
		}, 1000 * (i + 1));
	})(i);
}
```
在 JavaScript，參數是透過傳值方式給函數。所以原始的類型像是數字、日期、和字串基本上都是被複製的。如果你想要再函式內改變他們，它是不會影響外部的範圍。物件比較特別：假設內部函數改變屬性，這個改變會影響所有範圍。

其他解決方法可以使用 `let`。它是 `ES6` 其中一種變數的宣告方式，它和 `var` 不一樣，只在區塊內作用。

```js
for (let i = 0; i < 5; i++) {
	var temp = i;
 	setTimeout(function(){
		console.log(temp);
	}, 1000 * (i + 1));
}
```
