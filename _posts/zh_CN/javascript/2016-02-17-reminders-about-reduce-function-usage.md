---
layout: post

title: 怎样`reduce()`数组
tip-number: 48
tip-username: darul75
tip-username-profile: https://twitter.com/darul75
tip-tldr: 使用`reduce()`函数时的一些建议

redirect_from:
  - /zh_cn/reminders-about-reduce-function-usage/

categories:
    - zh_CN
    - javascript
---

文档里说`reduce()`方法接收一个函数作为累加器（accumulator），数组中的每个值（从左到右）开始合并，最终为一个值。

### `reduce()`

[reduce()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) 函数接收2个参数(M: 必填, O: 可选)：

- (M) 回调**reducer 函数** 处理先前的结算结果和下一个元素直到序列结束。
- (O) **初值** 作为第一次调用回调时的第一个参数。

所以，让我们先看一个普通用法，之后再看一个复杂用法。

### 普通用法 (累加，关联)

我们正在逛亚马逊(单价为美元$) 我们的购物车实在太满了，我们来计算一下总价吧：

```javascript
// 当前的购物清单
var items = [{price: 10}, {price: 120}, {price: 1000}];

// reducer函数
var reducer = function add(sumSoFar, nextPrice) { return sumSoFar + nextPrice.price; };

// 开始运行
var total = items.reduce(reducer, 0);

console.log(total); // 1130
```

`reduce`函数可选的参数在第一个例子里是基本变量数字0，但是它也可以是一个对象，数组... 而不仅是基本类型，之后我们将会看到。

现在，我们收到一个20$的优惠券。

```javascript
var total = items.reduce(reducer,-20);

console.log(total); // 1110
```

### 进阶用法(结合)

第二种用法的例子是`Redux`的[combineReducers](http://redux.js.org/docs/api/combineReducers.html)函数[源码](https://github.com/reactjs/redux/blob/master/src/combineReducers.js#L93)里用到的。

此创意是将`reducer`函数拆分为独立的函数，最后组合成一个新的*单一的大`reducer`函数*。 

为了说明，我们创建一个单一的对象，包含一些可以计算不同货币($, €...)的总价值的`reducer`函数。

```javascript
var reducers = {
  totalInDollar: function(state, item) {
    state.dollars += item.price;
    return state;
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
  // more...
};
```

然后我们建立一个瑞士军刀函数 

- 能够调用每一部分的`reduce`函数
- 返回一个新的`reducer`回调函数

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

现在，我们来看一下如何使用它。

```javascript
var bigTotalPriceReducer = combineTotalPriceReducers(reducers);

var initialState = {dollars: 0, euros:0, yens: 0, pounds: 0};

var totals = items.reduce(bigTotalPriceReducer, initialState);

console.log(totals);

/*
Object {dollars: 1130, euros: 1015.11531904, yens: 127524.24, pounds: 785.81131152}
*/
```

我希望这种方法可以使你在自己的需求内使用`reduce()`函数时有新的想法。

使用`reduce`函数也可以实现保存每一次计算结果的功能。这在`Ramdajs`里的[scan](http://ramdajs.com/docs/#scan)函数已经实现了。

[在JSFiddle里运行](https://jsfiddle.net/darul75/81tgt0cd/)
