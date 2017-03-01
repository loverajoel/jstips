---
layout: post

title: 仅用一行生成`[0, 1, ..., N-1]`数列
tip-number: 33
tip-username: SarjuHansaliya
tip-username-profile: https://github.com/SarjuHansaliya
tip-tldr: 我们可以创建一个函数，它可以仅用一行代码生成0...(N-1)数列。


redirect_from:
  - /zh_cn/create-range-0...n-easily-using-one-line/

categories:
    - zh_CN
    - javascript
---

使用下面一行代码，我们就可以生成0...(N-1)数列。

### 方法1 (需要 ES5)

```js
Array.apply(null, {length: N}).map(Function.call, Number);
```

#### 简要说明

1. `Array.apply(null, {length: N})` 返回一个由`undefined`填充的长度为`N`的数组(例如 `A = [undefined, undefined, ...]`)。
2. `A.map(Function.call, Number)` 返回一个长度为`N`的数组，它的索引为`I`的元素为`Function.call.call(Number, undefined, I, A)`的结果。
3. `Function.call.call(Number, undefined, I, A)`可转化为`Number(I)`，正好就是`I`。
4. 结果为：`[0, 1, ..., N-1]`。

更全面的介绍，请看[这里](https://github.com/gromgit/jstips-xe/blob/master/tips/33.md).

### 方法2 (需要 ES6)

这里用到了`Array.from` [https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/from](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/from)

```js
 Array.from(new Array(N),(val,index)=>index);
```

#### 简要说明

1. `A = new Array(N)` 返回一个有`N`个_小孔_的数组 (例如 `A = [,,,...]`, 但是对于`x` in `0...N-1`时`A[x] = undefined`)。
2. `F = (val,index)=>index` 即 `function F (val, index) { return index; }`。
3. `Array.from(A, F)` 返回一个长度为`N`的数组，它的索引为`I`的元素为`F(A[I], I)`的结果，也就是`I`。
4. 结果为：`[0, 1, ..., N-1]`。

### One More Thing

如果你需要[1, 2, ..., N]序列， **方法1** 可改为：

```js
Array.apply(null, {length: N}).map(function(value, index){
  return index + 1;
});
```

**方法2**可改为：

```js
Array.from(new Array(N),(val,index)=>index+1);
```