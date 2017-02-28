---
layout: post

title: 如何 reduce 陣列
tip-number: 48
tip-username: darul75
tip-username-profile: https://twitter.com/darul75
tip-tldr: 有關使用 `reduce` 函式的一些提醒。

redirect_from:
  - /zh_tw/reminders-about-reduce-function-usage/

categories:
    - zh_TW
    - javascript
---

正如官方文件所寫的，`reduce()` 方法接收一個函式做為累加器（accumulator），陣列中的每個值（由左到右）將會合併，最後只得到一個值。

### 署名

[reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) 函式接受 2 個參數（M：強制的，O：可選的）：

- (M) 一個 callback **reducer 函式** 可以處理先前的計算結果，到下一個元素直到最後。
- (O) 一個**初始值**可以被當作第一個呼叫 callback 的第一個參數。

所以讓我們來看一下普遍的用法，之後再看更多的複雜的用法。

### 普遍用法（累加、關聯）

我們在逛 Amazon 網站（價格為美元），但是我們的 caddy 太滿了，所以讓我們計算總價。

```javascript
// 我目前在 amazon 購買的 caddy
var items = [{price: 10}, {price: 120}, {price: 1000}];

// 我們的 reducer 函式
var reducer = function add(sumSoFar, item) { return sumSoFar + item.price; };

// 計算結果
var total = items.reduce(reducer, 0);

console.log(total); // 1130
```

我們在第一個事件，我們提供了 `reduce` 可選函式參數為一個整數 0，可以是一個物件、或是一個陣列，而不是原始的類型，之後我們將會看到。

現在，太酷了我得到一個 20$ 的折價券。

```javascript
var total = items.reduce(reducer, -20);

console.log(total); // 1110
```

### 進階用法（組合）

第二個使用範例的靈感是來自 Redux 的 [combineReducers](http://redux.js.org/docs/api/combineReducers.html) 函式，[原始碼](https://github.com/reactjs/redux/blob/master/src/combineReducers.js#L93)。

背後的想法是將 reducer 函式拆成獨立的函式，然後在最後計算出一個新的*單一 reducer 函式*。

如果要說明這些，讓我們建立一個單一物件和一些 reducers 函式可以計算不同的貨幣（$、€...）的總價。

```javascript
var reducers = {
  totalInDollar: function(state, item) {
    // 具體宣告...
    return state.dollars += item.price;
  },
  totalInEuros : function(state, item) {
    state.euros += item.price * 0.897424392;
    return state;
  },
  totalInPounds : function(state, item) {
    state.pounds += item.price * 0.692688671;
    return state;
  },
  totalInYen : function(state, item) {
    state.yens += item.price * 113.852;
    return state;
  }
  // 更多...
};
```

然後，我們建立一個新的多功能函式

- 負責應用每個部分的 reduce 函式。
- 回傳一個新的 callback reducer 函式。

```javascript
var combineTotalPriceReducers = function(reducers) {
  return function(state, item) {
    return Object.keys(reducers).reduce(
      function(nextState, key) {
        reducers[key](state, item);
        return state;
      },
      {}
    );
  }
};
```

現在讓我們看看如何使用它。

```javascript
var bigTotalPriceReducer = combineTotalPriceReducers(reducers);

var initialState = {dollars: 0, euros:0, yens: 0, pounds: 0};

var totals = items.reduce(bigTotalPriceReducer, initialState);

console.log(totals);

/*
Object {dollars: 1130, euros: 1015.11531904, yens: 127524.24, pounds: 785.81131152}
*/
```


我希望這種方法可以給你使用 reduce() 函數的時候提供另一個想法。

你的 reduce 函式可以處理每個計算的歷史記錄。這個在 Ramdajs 的 [scan](http://ramdajs.com/docs/#scan) 函式已經實現了。

[在 JSFiddle 試試看](https://jsfiddle.net/darul75/81tgt0cd/)
