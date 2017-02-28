---
layout: post

title: 可以接受单参数与数组的方法
tip-number: 06
tip-username: mattfxyz
tip-username-profile: https://twitter.com/mattfxyz
tip-tldr: 写一个方法可以接受单个参数也可以接受一个数组，而不是分开写两个方法。这和jQuery的一些方法的工作原理很像(`css` 可以修改任何匹配到的选择器).

redirect_from:
  - /zh_cn/writing-a-single-method-for-arrays-and-a-single-element/

categories:
    - zh_CN
    - javascript
---

写一个方法可以接受单个参数也可以接受一个数组，而不是分开写两个方法。这和jQuery的一些方法的工作原理很像(`css` 可以修改任何匹配到的选择器).

你只要把任何东西连接到一个数组. `Array.concat`可以接受一个数组也可以接受单个参数。

```javascript
function printUpperCase(words) {
  var elements = [].concat(words || []);
  for (var i = 0; i < elements.length; i++) {
    console.log(elements[i].toUpperCase());
  }
}
```


`printUpperCase`现在可以接受单个单词或多个单词的数组作为它的参数。同时也可以避免在不传递参数时抛出的`TypeError`错误的隐患。

```javascript
printUpperCase("cactus");
// => CACTUS
printUpperCase(["cactus", "bear", "potato"]);
// => CACTUS
//  BEAR
//  POTATO
```

