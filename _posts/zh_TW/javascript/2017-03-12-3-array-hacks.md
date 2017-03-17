---
layout: post

title: 使用 Array 的三個技巧
tip-number: 64
tip-username: hassanhelfi
tip-username-profile: https://twitter.com/hassanhelfi
tip-tldr: 在 JavaScript 中隨處都可以看見陣列，ECMAScript 6 介紹了展開運算符（spread operator），你可以透過它來處理陣列。在這篇 tip，我將示範三個有用的技巧，當你在寫程式時可以使用。

categories:
    - zh_TW
    - javascript
---

在 JavaScript 中隨處都可以看見陣列，ECMAScript 6 中介紹到了[展開運算符](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Spread_operator)，你可以透過它來處理陣列。在這篇 tip，我將示範三個有用的技巧，當你在寫程式時可以使用。

### 1. 迭代一個空的陣列

JavaScript 陣列特性是鬆散的，所以在這裡有許多坑。嘗試使用陣列的建構子建立一個陣列，你會明白我的意思。

```javascript
> const arr = new Array(4);
[undefined, undefined, undefined, undefined]
```

你可能發現到，迭代一個鬆散的陣列並應用在某些轉換是相當困難的。

```javascript
> const arr = new Array(4);
> arr.map((elem, index) => index);
[undefined, undefined, undefined, undefined]
```

為了解決這個問題，當你在建立陣列時你可以使用 `Array.apply`。

```javascript
> const arr = Array.apply(null, new Array(4));
> arr.map((elem, index) => index);
[0, 1, 2, 3]
```

### 2. 傳送一個空的參數到方法

如果你想要呼叫一個方法並忽略其中一個參數，如果你將參數為空的話，JavaScript 會告訴你發生錯誤。

```javascript
> method('parameter1', , 'parameter3');
Uncaught SyntaxError: Unexpected token ,
```

通常我們會採取傳送一個 `null` 或 `undefined` 的處理方式。

```javascript
> method('parameter1', null, 'parameter3') // 或者
> method('parameter1', undefined, 'parameter3');
```

我個人不喜歡使用 `null`，由於 JavaScript 會它當作一個 object，那是很奇怪的。隨著採用 ES6 的展開運算符，有一個更簡潔的方法將空參數傳送給方法。如我們先前所提到的，陣列的特性是鬆散的而且傳送空的值是可行的。我們將利用這個優勢來使用。

```javascript
> method(...['parameter1', , 'parameter3']); // 成功！
```

### 唯一的陣列值

我總是在想為什麼陣列建構子沒辦法指定的方法，方便的使用唯一的陣列值。展開運算符在這裡解救了我。使用展開運算符與 `Set` 建構子來產生唯一的陣列值。

```javascript
> const arr = [...new Set([1, 2, 3, 3])];
[1, 2, 3]
```
