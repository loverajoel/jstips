---
layout: post

title: 為什麼在做相等比較的時候，你應該使用 Object.is()
tip-number: 68
tip-username: TarekAlQaddy
tip-username-profile: https://github.com/TarekAlQaddy
tip-tldr: 在 JavaScript 中對於較鬆散的相等比較，有更好的解決方式

categories:
    - zh_TW
    - javascript
---

我們都知道 JavaScript 是一個較鬆散的型別，在某些情況它特別是在 `==` 的情況，當你透過 `==` 來做比較時，常常會得到意外的結果，基於這個原因我們會強制轉換或建立新的變數來「將兩個操作變數中的其中一個轉換為其他類型，然後進行比較」。

``` javascript
0 == ' ' //true
null == undefined //true
[1] == true //true
```

所以他們提供我們三等號 `===` 的相等操作符，它更嚴格而且不強制去轉換變數，然而 `===` 比較不是一個比較好的解決方式，你可以得到這樣的結果：

``` javascript
NaN === NaN //false
```

好消息是在 ES6 有一個新的 `Object.is()`，它是更精確而且和 `===` 有相同的功能，在某些特殊情況下也運作的很好：

``` javascript
Object.is(0 , ' '); //false
Object.is(null, undefined); //false
Object.is([1], true); //false
Object.is(NaN, NaN); //true
```

Mozilla 團隊 不認為 `Object.is` 比 `===` 更嚴格，他們宣稱我們應該思考這些方法如何處理 `NaN`、`-0` 和 `+0`，但是整體來說我認為它在實際的應用程式中是一個好的解決方式。

現在我們來看看這個比較表：

![differences of operators in equality comparisons javascript](http://i.imgur.com/pCyqkLc.png)

## 參考：
[Equality comparisons and sameness](http://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)
