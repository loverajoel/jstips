---
layout: post

title: 檢查屬性是否存在物件內
tip-number: 10
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: 這些方法都是檢查屬性是否存在目前的物件內。

redirect_from:
  - /zh_tw/check-if-a-property-is-in-a-object/

categories:
    - zh_TW
    - javascript
---

當你檢查屬性是否存在目前的[物件](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)內，你或許可以這麼做：

```javascript
var myObject = {
  name: '@tips_js'
};

if (myObject.name) { ... }

```

以上的方法是沒問題的，但是你必須知道對於這個問題有兩個原生的方法，[`in` 運算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in)和 [`Object.hasOwnProperty`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty)。任何繼承 `Object` 的都可以使用這兩種方法。

### 觀察之間較大的差別

```javascript
var myObject = {
  name: '@tips_js'
};

myObject.hasOwnProperty('name'); // true
'name' in myObject; // true

myObject.hasOwnProperty('valueOf'); // false, valueOf 繼承自原型鏈結
'valueOf' in myObject; // true

```

兩者不同的地方在於確認的屬性深度不同。換句話說，如果直接在物件內確認 key 是可用的話，`hasOwnProperty` 只會回傳 true。然而，在 `in` 運算符沒辦法分辨之間的屬性是建立在物件或是繼承自原型鏈結的。

這裡有其他的範例：

```javascript
var myFunc = function() {
  this.name = '@tips_js';
};
myFunc.prototype.age = '10 days';

var user = new myFunc();

user.hasOwnProperty('name'); // true
user.hasOwnProperty('age'); // false, 因為 age 是繼承自原型鏈結
```

在[線上範例](https://jsbin.com/tecoqa/edit?js,console)確認吧！
確認屬性是否存在在物件內的問題常見錯誤，我推薦閱讀關於這個問題的[討論](https://github.com/loverajoel/jstips/issues/62)。
