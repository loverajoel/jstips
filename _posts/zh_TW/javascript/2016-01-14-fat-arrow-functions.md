---
layout: post

title: 箭頭函式
tip-number: 14
tip-username: pklinger
tip-username-profile: https://github.com/pklinger/
tip-tldr: 介紹一個 ES6 的新特性 - 箭頭函式是一個方便的語法讓你用更少的程式碼做更多事。

redirect_from:
  - /zh_tw/fat-arrow-functions/

categories:
    - zh_TW
    - javascript
---

介紹一個 ES6 的新特性 - 箭頭函式，它是一個方便的語法讓你用更少的程式碼做更多事。它的名稱來自它的語法，`=>`，它是一個「fat arrow」， 相較於 `->`。有些開發者或許已經知道這個類型的函式是從不同的程式語言來的，像是 Haskell，作為「lambda 表達式」或者是「匿名函式」。它被稱作匿名函式是因為沒有一個名稱作為函數的名稱。

### 這有什麼好處？
* 語法：更少的程式碼；不需要重複再打出 `function`。
* 語義：從上下文（contex）取得 `this`。

### 簡單的語法範例
你可以觀察這兩個程式碼的片段，它們做的是相同的工作，你很快地可以了解到箭頭函式做了什麼：

```javascript
// 箭頭函式的一般語法
param => expression

// 也可以寫入括號
// 在多個參數時，括號是必須的
(param1 [, param2]) => expression


// 使用函式
var arr = [5,3,2,9,1];
var arrFunc = arr.map(function(x) {
  return x * x;
});
console.log(arr)

// 使用箭頭函式
var arr = [5,3,2,9,1];
var arrFunc = arr.map((x) => x*x);
console.log(arr)
```

正如你所見的，在這個範例箭頭函式省去了打出函式的括號和 return。我建議你在參數周圍寫出小括號，如果你需要多個輸入參數，像是 `(x, y) => x + y`。這是一個用來應付在不同情況下忘記使用小括號的方法。上面的程式碼也是這樣執行的：`x => x * x`。到目前為止，這些只是語法上的改進，減少的程式碼以及提高可讀性。

### 詞彙綁定 - `this`

這是一個另一個更棒的理由來使用箭頭函式。這裡有一個 `this` context 的問題。使用箭頭函數，你不需要擔心 `.bind(this)` 或設定 `that = this` 的問題了，在箭頭函式會幫你從詞彙的範圍綁定 `this` 的 context。看以下的[範例](https://jsfiddle.net/pklinger/rw94oc11/)：

```javascript

// 在全域定義 this.i
this.i = 100;

var counterA = new CounterA();
var counterB = new CounterB();
var counterC = new CounterC();
var counterD = new CounterD();

// bad example
function CounterA() {
  // CounterA 的 `this` 實例（！！這裡被忽略了）
  this.i = 0;
  setInterval(function () {
    // `this` 參考到全域的物件，而不是 CounterA's 的 `this`，
    // 因此，起始的計數是 100，而不是 0（CounterA 的 this.i）。
    this.i++;
    document.getElementById("counterA").innerHTML = this.i;
  }, 500);
}

// 手動綁定 that = this
function CounterB() {
  this.i = 0;
  var that = this;
  setInterval(function() {
    that.i++;
    document.getElementById("counterB").innerHTML = that.i;
  }, 500);
}

// 使用 .bind(this)
function CounterC() {
  this.i = 0;
  setInterval(function() {
    this.i++;
    document.getElementById("counterC").innerHTML = this.i;
  }.bind(this), 500);
}

// 箭頭函式
function CounterD() {
  this.i = 0;
  setInterval(() => {
    this.i++;
    document.getElementById("counterD").innerHTML = this.i;
  }, 500);
}
```

更多關於箭頭函式的資訊你可以在 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) 找到。如果查看不同的語法選項拜訪[這個網站](http://jsrocks.org/2014/10/arrow-functions-and-their-scope/)。
