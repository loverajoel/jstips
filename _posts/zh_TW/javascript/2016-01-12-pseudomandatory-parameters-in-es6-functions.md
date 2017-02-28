---
layout: post

title: 在 ES6 函式內的預設參數
tip-number: 12
tip-username: Avraam Mavridis
tip-username-profile: https://github.com/AvraamMavridis
tip-tldr: 在許多程式設計語言函數的參數預設是強制需要的，而開發者也會明確定義一個可選的參數。

redirect_from:
  - /zh_tw/pseudomandatory-parameters-in-es6-functions/

categories:
    - zh_TW
    - javascript
---

在許多程式設計語言函數的參數預設值是強制需要的，而開發者也會明確定義一個可選的參數。在 JavaScript 中，每個參數都是可選的，利用 [**es6 參數預設值**](http://exploringjs.com/es6/ch_parameter-handling.html#sec_parameter-default-values)的特性，我們可以強制執行這個行為，而不會弄亂函數的主體。

```javascript
const _err = function( message ){
  throw new Error( message );
}

const getSum = (a = _err('a is not defined'), b = _err('b is not defined')) => a + b

getSum( 10 ) // 拋出錯誤，b 沒有被定義
getSum( undefined, 10 ) // 拋出錯誤，a 沒有被定義
```

 `_err` 是一個函式可以立即拋出錯誤。如果沒有傳送其中一個參數，函數預設值就會被使用，`_err` 將會被呼叫而且會拋出錯誤。你可以在 [Mozilla's Developer Network ](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/default_parameters) 看更多關於 **預設參數值特性** 的範例。
