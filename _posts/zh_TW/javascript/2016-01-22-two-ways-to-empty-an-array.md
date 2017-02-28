---
layout: post

title: 將陣列清空的兩種方法
tip-number: 22
tip-username: microlv
tip-username-profile: https://github.com/microlv
tip-tldr: 在 JavaScript 中當你相要清空陣列，有許多方法，但這是最具效能的方法。

redirect_from:
  - /zh_tw/two-ways-to-empty-an-array/

categories:
    - zh_TW
    - javascript
---

你定義了一個陣列然後你想清空陣列內的內容。
通常你會這麼做：

```javascript
// 定義陣列
var list = [1, 2, 3, 4];
function empty() {
    // 清空陣列
    list = [];
}
empty();
```
但是這裡有另一個更能具效能的清空陣列的方式。

你應該像這樣使用程式碼：

```javascript
var list = [1, 2, 3, 4];
function empty() {
    // 清空陣列
    list.length = 0;
}
empty();
```

* `list = []` 將分配一個新的參考陣列給變數，而其他的參考則不受影響。
這個意思是說，前面參考的陣列內容還存在記憶體中，導致記憶體洩漏。

* `list.length = 0` 刪除陣列內所有的內容，也會影響到其他的參考。

換句話說，假設你有兩個變數且參考到同一個陣列（`a = [1,2,3]; a2 = a;`），而你使用 `list.length = 0` 刪除陣列的內容，兩個參考（a 和 a2）將指向相同的空陣列。（如果你不想讓 a2 內容變成空的陣列，請不要使用這個方法！）

思考一下這些會輸出什麼：

```js
var foo = [1,2,3];
var bar = [1,2,3];
var foo2 = foo;
var bar2 = bar;
foo = [];
bar.length = 0;
console.log(foo, bar, foo2, bar2);

// [] [] [1, 2, 3] []
```

在 Stackoverflow 了解更多的細節：
[difference-between-array-length-0-and-array](http://stackoverflow.com/questions/4804235/difference-between-array-length-0-and-array)
