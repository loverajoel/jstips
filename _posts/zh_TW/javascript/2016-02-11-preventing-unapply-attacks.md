---
layout: post

title: 防止 Unapply 攻擊
tip-number: 42
tip-username: emars
tip-username-profile: https://twitter.com/marseltov
tip-tldr: 凍結內建的屬性。

redirect_from:
  - /zh_tw/preventing-unapply-attacks/

categories:
    - zh_TW
    - javascript
---

透過覆寫內建的原型，攻擊者可以重寫程式碼來暴露或更改綁定的參數。這是一個嚴重的安全漏洞，利用 es5 polyfill 的方法。

```js
// 綁定 polyfill 範例
function bind(fn) {
  var prev = Array.prototype.slice.call(arguments, 1);
  return function bound() {
    var curr = Array.prototype.slice.call(arguments, 0);
    var args = Array.prototype.concat.apply(prev, curr);
    return fn.apply(null, args);
  };
}


// unapply 攻擊
function unapplyAttack() {
  var concat = Array.prototype.concat;
  Array.prototype.concat = function replaceAll() {
    Array.prototype.concat = concat; // 恢復正確的版本
    var curr = Array.prototype.slice.call(arguments, 0);
    var result = concat.apply([], curr);
    return result;
  };
}
```

以上的函式拋棄了綁定的 `prev` 陣列，任何 `.concat` 在第一個 `concat` 被呼叫之後使用 unapply 攻擊會拋出錯誤。

使用 [Object.freeze](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze) 讓物件保持不變，你可以防止任何內建物件原型被覆寫。


```js
(function freezePrototypes() {
  if (typeof Object.freeze !== 'function') {
    throw new Error('Missing Object.freeze');
  }
  Object.freeze(Object.prototype);
  Object.freeze(Array.prototype);
  Object.freeze(Function.prototype);
}());
```

你可以在[這裡](https://glebbahmutov.com/blog/unapply-attack/)閱讀更多關於 unapply 攻擊。
