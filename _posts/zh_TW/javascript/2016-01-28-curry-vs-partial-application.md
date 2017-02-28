---
layout: post

title: 柯里化（currying）和部分應用程式
tip-number: 28
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: 柯里化（currying）和部分應用程式（partial application）是將函式轉換成一般較小的 arity 和另一個函式的兩種方式。


redirect_from:
  - /zh_tw/curry-vs-partial-application/

categories:
    - zh_TW
    - javascript
---

**柯里化**

柯里化是將一個函式

`f: X * Y -> R`

轉換成

`f': X -> (Y -> R)`

而不是帶有兩個參數的 `f'`，我們調用 `f'` 與第一個參數。其結果是一個函式，我們可以呼叫第二個參數來產生結果。

因此，未使用柯里化的函式 `f` 像這樣調用：

`f(3, 5)`

如果使用柯里化後的函式 `f'` 像這樣調用：

`f(3)(5)`

例如：
尚未柯里化的函式 `add()`

```javascript

function add(x, y) {
  return x + y;
}

add(3, 5);   // returns 8
```

柯里化後的函式 `add()`

```javascript
function addC(x) {
  return function (y) {
    return x + y;
  }
}

addC(3)(5);   // returns 8
```

**柯里化的規則**

柯里化將一個二元函式轉換成一個一元函式，這個一元函式再回傳一個一元函式。

柯里化：`(X × Y → R) → (X → (Y → R))`

JavaScript 程式碼：

```javascript
function curry(f) {
  return function(x) {
    return function(y) {
      return f(x, y);
    }
  }
}
```

**部分應用程式**

部分應用程式將一個函式的

f：`X * Y -> R`

第一個參數固定來產生新的函式

f'：`Y -> R`

`f'` 和 `f` 不同，只需要填寫第二個參數，這也是為什麼 `f'` 比 `f` 少一個參數的原因。

例如：綁定函式的第一個參數來產生函式 `plus5`。

```javascript
function plus5(y) {
  return 5 + y;
}

plus5(3);  // returns 8
```

**部分應用程式的規則**

部分應用程式將二元函式和數值產生一個一元函式。

部分應用程式: `((X × Y → R) × X) → (Y → R)`

Javascript 程式碼：

```javascript
function partApply(f, x) {
  return function(y) {
    return f(x, y);
  }
}
```
