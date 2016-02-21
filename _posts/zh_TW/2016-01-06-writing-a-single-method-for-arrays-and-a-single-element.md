---
layout: post

title: 撰寫一個可以接受單一參數和陣列的方法
tip-number: 06
tip-username: mattfxyz
tip-username-profile: https://twitter.com/mattfxyz
tip-tldr: 撰寫你的函式可以處理陣列或單一元素參數，而不是透過分開的方法來處理陣列和單一元素參數。這和 jQuery 一些函式工作原理相似（`css` selector 將會修改所有匹配的）。

categories:
    - zh_TW
---

撰寫你的函式可以處理陣列或單一元素參數，而不是透過分開的方法來處理陣列和單一元素參數。這和 jQuery 一些函式工作原理相似（`css` selector 將會修改所有匹配的）。

首先，你只要將任何的東西 concat 到陣列上。`Array.concat` 將會接受陣列或是單一元素。

```javascript
function printUpperCase(words) {
  var elements = [].concat(words);
  for (var i = 0; i < elements.length; i++) {
    console.log(elements[i].toUpperCase());
  }
}
```

`printUpperCase` 現在已經可以接收單一文字或是多個文字的陣列當作它的參數了。

```javascript
printUpperCase("cactus");
// => CACTUS
printUpperCase(["cactus", "bear", "potato"]);
// => CACTUS
//  BEAR
//  POTATO
```
