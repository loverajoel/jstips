---
layout: post

title: Truncating 最快的方式（含有風險）
tip-number: 18
tip-username: pklinger
tip-username-profile: https://github.com/pklinger
tip-tldr: 通常 `~~X` 速度比 `Math.trunc(X)` 快，但是會造成你的程式碼變得很混亂。

redirect_from:
  - /zh_tw/rounding-the-fast-way/

categories:
    - zh_TW
    - javascript
---

今天的 tip 是關於性能的部分。

[曾經使用過雙波浪](http://stackoverflow.com/questions/5971645/what-is-the-double-tilde-operator-in-javascript) `~~` 運算符嗎？有時候也被稱為 雙 NOT 位元運算符。你可以使用它來替代 `Math.trunc()` 更為快速。這是為什麼呢？

位元移位運算符 `~` 將輸入的 32 位元轉換成 `-(input + 1)`。因此，雙位元移位運算成為更好的工具，將輸入轉換成 `-(-(input + 1) + 1)` 更趨近 0。對於數字輸入，它類似 `Math.trunc()`。若失敗的話，則回傳 `0`，這或許是解決 `Math.trunc()` 失敗時回傳 `NaN` 的替代方法。

```js
// 單 ~
console.log(~1337)    // -1338

// 數字輸入
console.log(~~47.11)  // -> 47
console.log(~~1.9999) // -> 1
console.log(~~3)      // -> 3
```

雖然 ~~ 可以讓性能更好，但是為了增加程式碼可讀性，請使用 Math.trunc()。如果要了解為什麼，這裡有一些關於 `~~` 運算子的分析。

### 適用情況

##### 每個 CPU 的週期次數
`~~` 整體來說或許比 `Math.trunc()` 來的快，這種[測試的假設](https://jsperf.com/jsfvsbitnot/10)在哪個平台下是很重要的。此外，你通常必須執行數以百萬計的這種操作才可以看到明顯的影響。

##### 當程式碼的清晰度不是這麼重要時
如果你想要 confuse 他人，或者從你的 minifier/uglifier 取得最大的效用，這是一個相對廉價的方式。

### 禁止的情況

##### 當你的程式碼需要維護時

程式碼的清晰是一直以來都是相當重要的，無論你是不是和一個團隊一起工作，或是對公開的 repo 做 contribute。正如[俗話常說的](http://c2.com/cgi/wiki?CodeForTheMaintainer)：
> Always code as if the person who ends up maintaining your code is a violent psychopath who knows where you live.

##### 當你忘記 `~~` 總是趨近於零時
或許新手開發者更關注在 `~~` 優秀之處，卻忘記了「只去掉小數點」的重要性。當我們將浮點數轉換成陣列索引，或是相關順序值，這容易導致 **fencepost 錯誤**（a.k.a 「off-by-one」），實際上可能需要不同類型的分數做四捨五入（程式碼缺乏清晰度很容易造成這個問題。）

舉個例子，如果你基於在「最靠近整數」的數字上做計算，你應該使用 `Math.round()` 而不是 `~~`，但因為開發者的懶惰往往勝過於冰冷的邏輯，而導致不正確的結果。

相反的，許多名稱類似 `Math.xyz()` 的函式反而清楚表達他們的功用，減少了錯誤的可能性。

##### 當處理大量的位元數時
因為 `~` 首先是進行 32 位元的轉換，`~~` 範圍值的結果在 &plusmn;2.15 億位元左右。如果你沒有明確的檢查你的輸入範圍，當轉換後的值和原始值有很大的差距時，使用者可能會觸發 unexpected 的行為：

```js
a = 2147483647.123  // 最大 32 位正整數，再多一點
console.log(~~a)    // ->  2147483647     (ok)
a += 10000          // ->  2147493647.123 (ok)
console.log(~~a)    // -> -2147483648     (huh?)
```
一個容易出現問題的地方是在處理 Unix 時間戳記的地方（以秒為單位，從 1970 年 1 月 1 日 00:00:00 UTC）。一個快速取得這個值的方式是：

```js
epoch_int = ~~(+new Date() / 1000)  // Date() 以毫秒為單位
```
然而，當我們處理在 2038 年 1 月 19 03:14:07 UTC（有時候稱為 **Y2038 limit**）之後的時間戳記，發生可怕的事：

```js
// 2040 年 1 月 1 日 00:00:00.123 UTC 的時間戳記
epoch = +new Date('2040-01-01') / 1000 + 0.123      // ->  2208988800.123

// 回到未來！
epoch_int = ~~epoch                                 // -> -2085978496
console.log(new Date(epoch_int * 1000))             // ->  Wed Nov 25 1903 17:31:44 UTC

// 這很有趣，讓我們取得正確的答案
epoch_flr = Math.floor(epoch)                       // ->  2208988800
console.log(new Date(epoch_flr * 1000))             // ->  Sun Jan 01 2040 00:00:00 UTC
```

##### 當原始輸入值沒經過處理
因為 `~~` 將每個非數字轉換成 `0`：

```js
console.log(~~[])   // -> 0
console.log(~~NaN)  // -> 0
console.log(~~null) // -> 0
```
有些開發者把它作為替代輸入驗證。然而，這可能會導致奇怪的邏輯錯誤，你沒辦法區別他們之間誰是無效的輸入，或者是 `0`。因此這_不是_推薦的做法。

##### 當許多人認為 `~~X == Math.floor(X)` 時

許多人因為錯誤的原因以為「雙位元 NOT」等同於 `Math.floor()`。如果你沒辦法準確的使用它，最終你可能會濫用它。
有些人很細心地提到 `Math.floor()` 是用在正數輸入，而 `Math.ceil()` 是用在負數輸入。但是，這又會強制讓你停下並思考關於你該如何處理數值。這違背了使用 `~~` 做為方便無害的目的。

### 結論
避免在可能的情況。否則請謹慎使用。

### 管理
1. 謹慎使用。
2. 在應用前請先處理數值。
3. 仔細記錄關於數值被轉換的相關假設。
4. 至少檢查程式碼並處理：
   * 不正確輸入反而傳送給其他程式碼模組作為有效的 `0` 的邏輯 Bug。
   * 在轉換輸入的範圍錯誤。
   * 因為不正確的四捨五入方向，造成 fencepost 錯誤。
