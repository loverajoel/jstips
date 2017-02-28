---
layout: post

title: 了解傳送機制
tip-number: 44
tip-username: bmkmanoj
tip-username-profile: https://github.com/bmkmanoj
tip-tldr: JavaScript 技術上只傳送原始和物件類型的值（或參考）。在參考的類型下，參考值本身是 passed by value。

redirect_from:
  - /zh_tw/know-the-passing-mechanism/

categories:
    - zh_TW
    - javascript
---
JavaScript 技術上是透過 pass-by-value。它既不是傳值（pass-by-value）也不是傳參考（pass-by-reference），要理解這些術語的意義，你要了它們傳送的機制，透過以下的範例程式碼和解釋了解它們的意義。

### 範例一

```js

var me = {					// 1
	'partOf' : 'A Team'
};

function myTeam(me) {		// 2

	me = {					// 3
		'belongsTo' : 'A Group'
	};
}

myTeam(me);
console.log(me);			// 4  : {'partOf' : 'A Team'}

```

在上方的範例，當 `myTeam` 函式被調用，JavaScript *將 `me` 物件當作 passing the reference 作為值*，調用本身建立了兩個獨立的參考在相同的物件，（雖然在這邊名稱相同，例如 `me`，這是一個誤導讓我們以為它是單一參考物件的印象。），因此，參考變數它們都是獨立的。

當我們在 #`3` 給了一個新的物件，我們完全改變 `myTeam` 函式內的參考值，在函式之外的原始物件不會受到影響，從這裡物件參考到外部保留了原始物件的值，並傳入函式內，因此可以從 #`4` 看到輸出值。


### 範例二

```js

var me = {					// 1
	'partOf' : 'A Team'
};

function myGroup(me) { 		// 2
	me.partOf = 'A Group';  // 3
}

myGroup(me);
console.log(me);			// 4  : {'partOf' : 'A Group'}

```

在這個例子 `myGroup` 被調用，我們傳送了物件 `me`。但不像範例一的程式碼，我們沒有給予 `me` 變數到任何的新物件，當我們在 `myGroup` 函式內修改物件的屬性，物件參考值一直是參考到原始的值，這是可以有效的改變物件的屬性。因此你可以從 #`7` 看到輸出值。

所以最後一個情況也不能證明 JavaScript 是 pass-by-reference 嗎？不，它不是的。記住，*如果是物件的情況下，JavaScript 將 passes the reference 作為值*。這裡會產生困惑，所以我們往往不能完全理解什麼是傳參考。這是明確的原因，有些人喜歡稱它們為 *call-by-sharing*。


*本文最早被作者發表於 [js-by-examples](https://github.com/bmkmanoj/js-by-examples/blob/master/examples/js_pass_by_value_or_reference.md)*
