---
layout: post

title: 使用「new」運算符的回傳值
tip-number: 52
tip-username: Morklympious
tip-username-profile: https://github.com/morklympious
tip-tldr: 當使用 new 和不使用 new 時，了解他們所回傳的值。

redirect_from:
  - /zh_tw/return-values-with-the-new-operator/

categories:
    - zh_TW
    - javascript
---

在 JavaScript 你會碰到一些情況，使用 `new` 來分配新的物件。這會打斷你的思維，除非你閱讀這篇 tip 來了解到底在背後發生了哪些事。

在合理情況下，JavaScript 中的 `new` 是一個運算符，回傳一個新的物件實例，假設我們有一個建構函式：

````js
function Thing() {
  this.one = 1;
  this.two = 2;
}

var myThing = new Thing();

myThing.one // 1
myThing.two // 2
````

__注意__：除此之外，如果 `Thing()` 沒有透過 `new` 來呼叫的話，_沒有物件會被建立_，`this` 會指向到全域物件 window。這個意思就是：

1. 你突然會有兩個全域變數叫作 `one` 和 `two`。
2. `myThing` 現在是 undefined，因為在 `Thing()` 沒有任何的回傳。

現在這個範例中，有些東西有點令人疑惑。比方我說加入建構函式：

````js
function Thing() {
  this.one = 1;
  this.two = 2;

  return 5;
}

var myThing = new Thing();
````

現在 myThing 等於多少？是 5 嗎？它不是一個物件嗎？還是自我的缺少感？可能永遠都不知道！

除了我們可知道的是：

````js
myThing.one // 1
myThing.two // 2
````

更有趣的是，我們從來都沒看到從我們建構子中「回傳」的 5 。真是奇怪，到底怎麼了？function 你到底在做什麼呀 ？我的 5 呢？讓我來嘗試一些東西。

讓我們回傳一個非原始類型來做取代，像是一個物件。

````js
function Thing() {
  this.one = 1;
  this.two = 2;

  return {
    three: 3,
    four: 4
  };
}

var myThing = new Thing();
````

讓我們來確認一下，快速的 console.log 透露了所有訊息：

````js
console.log(myThing);
/*
  Object {three: 3, four: 4}
  this.one and this.two 發生了什麼事！？
  我的朋友呀，他們被蓋掉了。
*/
````

__在這裡我們可以學到：__ 當你調用一個有 `new` keyword 的函式，你可以使用 `this` 來設定屬性（但是你可能已經知道這些了）。從 `new` keyword 你呼叫了函式，所回傳的值不是你所指定的值，而是將函式的 `this` 實例回傳（你所放的屬性，像是 `this.one = 1`;）。

然而，回傳一個非原始值，像是 `object`、`array` 或者是 `function` 會覆蓋在 `this` 這個實例，將會破壞原本你所分配給 `this` 的值。
