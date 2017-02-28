---
layout: post

title: 使用一行程式碼建立一個 `[0, 1, ..., N - 1]` 的陣列
tip-number: 33
tip-username: SarjuHansaliya
tip-username-profile: https://github.com/SarjuHansaliya
tip-tldr: 使用一行程式碼，來產生有順序性的陣列。


redirect_from:
  - /zh_tw/create-range-0...n-easily-using-one-line/

categories:
    - zh_TW
    - javascript
---

這裡有兩種 compact 程式碼序列方式，來產生一個 `[0, 1, ..., N-1]` 的 `N` 個元素的陣列：

### 方法一（ES5）

```js
Array.apply(null, {length: N}).map(Function.call, Number);
```

#### 簡要說明

1. `Array.apply(null, {length: N)` 回傳一個 `N` 個元素的陣列，裡面陣列元素都是為 `undefined`（i.e. `A = [undefined, undefined, ...]`）。
2. `A.map(Function.call, Number)` 回傳一個 `N` 個元素的陣列，索引 `I` 從 `Function.call.call(Number, undefined, I, A)` 取得結果。
3. `Function.call.call(Number, undefined, I, A)` 轉變成 `Number(I)`，這剛好就是 `I`。
4. 結果：`[0, 1, ..., N-1]`。

更深入的解釋，請前往[這裡](https://github.com/gromgit/jstips-xe/blob/master/tips/33.md)。

### 方法二（ES6）

```js
Array.from(new Array(N), (val, index) => index);
```

#### 簡要說明

1. `A = new Array(N)` 回傳一個有 `N` 個 _holes_ 的陣列（i.e. `A = [,,,...]`，但是 `x` 在 `0...N-1` 時 `A[x] = undefined`）。
2. `F = (val, index) => index` 等同於 `function F (val, index) { return index; }`。
3. `Array.from(A, F)` 回傳一個 `N` 個元素的陣列，索引 `I` 取得 `F(A[I], I)` 的結果，也就是 `I`。
4. 結果：`[0, 1, ..., N-1]`。

### 還有一件事情

如果你真的想要排序 [1, 2, ..., N]，**方法一**改為：

```js
Array.apply(null, {length: N}).map(function(value, index){
  return index + 1;
});
```

和 **方法二**：

```js
Array.from(new Array(N), (val, index) => index + 1);
```
