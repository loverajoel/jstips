---
layout: post

title: JavaScript 中的捷徑計算
tip-number: 27
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: 捷徑計算意思是說，假設第一個參數不足以確定表達式的值，第二個參數才會被執行，當 AND 函數的第一個參數計算結果為 false，則所有結果則為 false；當 OR 函數的第一個參數計算結果為 true，則所有結果為 true。

redirect_from:
  - /zh_tw/short-circiut-evaluation-in-js/

categories:
    - zh_TW
    - javascript
---

[捷徑計算](https://en.wikipedia.org/wiki/Short-circuit_evaluation)意思是說，假設第一個參數不足以確定表達式的值，第二個參數才會被執行，當 AND 函數的第一個參數計算結果為 false，則所有結果則為 false；當 OR 函數的第一個參數計算結果為 true，則所有結果為 true。

對於以下的 `test` 條件和 `isTrue` 以及 `isFalse` 函式。

```js
var test = true;
var isTrue = function(){
  console.log('Test is true.');
};
var isFalse = function(){
  console.log('Test is false.');
};

```
使用 AND 邏輯 - `&&`。

```js
// 一個正常的 if 條件式
if (test){
  isTrue();    // Test 是 true
}

// 上面可以使用 '&&' 作為 -

( test && isTrue() );  // Test 是 true
```
使用 OR 邏輯 - `||`。

```js
test = false;
if (!test){
  isFalse();    // Test 是 false.
}

( test || isFalse());  // Test 是 false.
```
OR 邏輯可以用在為函式參數設定預設值。

```js
function theSameOldFoo(name){
    name = name || 'Bar' ;
    console.log("My best friend's name is " + name);
}
theSameOldFoo();  // My best friend's name is Bar
theSameOldFoo('Bhaskar');  // My best friend's name is Bhaskar
```
當屬性尚未被定義的時候，邏輯 AND 可以避免異常情況。
例如：

```js
var dog = {
  bark: function(){
     console.log('Woof Woof');
   }
};

// 呼叫 dog.bark();
dog.bark(); // Woof Woof.

// 但是如果 dog 尚未被定義，dog.bark() 將會發生「無法讀取尚未定義的屬性 'bark'」的錯誤。
// 為了防止這個問題，我們使用 &&。

dog && dog.bark(); // 如果 dog 被定義了，那我們就可以呼叫 dog.bark()。

```
