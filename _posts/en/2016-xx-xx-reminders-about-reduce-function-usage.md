---
layout: *post

title: Reduce builtin function usage
tip-number: xx
tip-username: darul75
tip-username-profile: https://twitter.com/darul75
tip-tldr: some reminders about using the reduce function

categories:
    - en
---

As written in documentation the reduce() method applies a function against an accumulator and each value of the array (from left-to-right) 
to reduce it to a single value.

reduce() function accepts 2 parameters (M: mandatory, O: optional):

- (M) a callback **reducer function** to be applied that deals with a pair of previous (result of previous computation) and next element until end of the list.
- (O) an **initial value** to be used as the first argument to the first call of the callback.

So let's see a common usage and later a more sophisticated one.

### Common usage (accumulation, concatenation)

We are on Amazon website (prices in $) and our caddy is quite full, let's compute total.

```javascript
// my current amazon caddy purchases
var items = [{price: 10}, {price: 120}, {price: 1000}];

// our reducer function
var reducer = function add(sumSoFar, nextPrice) { return sumSoFar + nextPrice.price; };

// do the job
var total = items.reduce(reducer, 0);

console.log(total); // 1130
```

Optional reduce function parameter was primitive integer type 0 in that first case, but it could have been an Object, an Array...instead of a primitive type,
but we will see that later.

Now, cool I received a discount coupon of 20$.

```javascript
var total = items.reduce(reducer,-20);

console.log(total); // 1110
```

### Advanced usage (combination)

This second usage example is inspired by Redux [combineReducers](http://redux.js.org/docs/api/combineReducers.html) function [source](https://github.com/reactjs/redux/blob/master/src/combineReducers.js#L93).

Idea behind is to separate reducer function into separate individual functions and at the end compute a new *single big reducer function*. 

To illustrate this, let's create a single object literal with some reducers function able to compute total prices in different currency $, €...

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

Then, we create a new swiss knife function 

- responsible for applying each partial reduce functions.
- that will return a new callback reducer function

```javascript
var combineTotalPriceReducers = function(reducers, initialState) {
  return function(state, item) {
    return Object.keys(reducers).reduce(
      function(nextState, key) {
        reducers[key](nextState, item);
        return nextState;
      },
      initialState
    );
  }
};
```

Now let's see how using it.

```javascript
var firstPrice = items[0].price;

var initialState = {dollars: firstPrice, euros:firstPrice, yens: firstPrice, pounds: firstPrice};

var bigTotalPriceReducer = combineTotalPriceReducers(reducers, initialState);

var totals = items.reduce(bigTotalPriceReducer);

console.log(totals);

/*
Object {dollars: 1130, euros: 1015.11531904, yens: 127524.24, pounds: 785.81131152}
*/
```

I hope this approach can give you another idea of using reduce() function for your own needs.

Your reduce function could handle an history of each computation by instance as it is done in Ramdajs with [scan](http://ramdajs.com/docs/#scan) function

[JSFiddle to play with](https://jsfiddle.net/darul75/81tgt0cd/)