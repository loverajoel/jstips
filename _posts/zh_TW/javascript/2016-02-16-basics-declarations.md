---
layout: post

title: 宣告的基本知識
tip-number: 47
tip-username: adaniloff
tip-username-profile: https://github.com/adaniloff
tip-tldr: 了解並處理宣告。

redirect_from:
  - /zh_tw/basics-declarations/

categories:
    - zh_TW
    - javascript
---

以下有不同的 JavaScript 變數宣告方式。
註解和 `console.log` 應該可以足夠解釋在這裡發生了什麼：

```js
var y, x = y = 1 //== var x; var y; x = y = 1
console.log('--> 1:', `x = ${x}, y = ${y}`)

// 將會印出
//--> 1: x = 1, y = 1
```

首先，我們只是設定兩個變數，沒有其他的變數。

```js
;(() => {
  var x = y = 2 // == var x; x = y = 2;
  console.log('2.0:', `x = ${x}, y = ${y}`)
})()
console.log('--> 2.1:', `x = ${x}, y = ${y}`)

// 將會印出
//2.0: x = 2, y = 2
//--> 2.1: x = 1, y = 2
```

你可以看到，程式碼只改變了全域的 y，因為我們還沒有宣告變數在 closure。

```js
;(() => {
  var x, y = 3 // == var x; var y = 3;
  console.log('3.0:', `x = ${x}, y = ${y}`)
})()
console.log('--> 3.1:', `x = ${x}, y = ${y}`)

// 將會印出
//3.0: x = undefined, y = 3
//--> 3.1: x = 1, y = 2
```

現在我們透過 var 來宣告兩個變數。意思說它們只存在 closure 的 context。

```js
;(() => {
  var y, x = y = 4 // == var x; var y; x = y = 4
  console.log('4.0:', `x = ${x}, y = ${y}`)
})()
console.log('--> 4.1:', `x = ${x}, y = ${y}`)

// 將會印出
//4.0: x = 4, y = 4
//--> 4.1: x = 1, y = 2
```

兩個變數已經使用 var 宣告，也設定了他們的值。既然 `local > global`，x 和 y 在 closure 內，意思說全域的 x 和 y 是不會改變的。

```js
x = 5 // == x = 5
console.log('--> 5:', `x = ${x}, y = ${y}`)

// 將會印出
//--> 5: x = 5, y = 2
```

最後的結果是很明顯的。

你可以測試這些程式碼並觀看結果，[感謝 babel](https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=var%20y%2C%20x%20%3D%20y%20%3D%201%20%2F%2F%3D%3D%20var%20x%3B%20var%20y%3B%20x%20%3D%20y%20%3D%201%0Aconsole.log('--%3E%201%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%0A%2F%2F%20Will%20print%0A%2F%2F--%3E%201%3A%20x%20%3D%201%2C%20y%20%3D%201%0A%0A%3B(()%20%3D%3E%20%7B%20%0A%20%20var%20x%20%3D%20y%20%3D%202%20%2F%2F%20%3D%3D%20var%20x%3B%20y%20%3D%202%3B%0A%20%20console.log('2.0%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%7D)()%0Aconsole.log('--%3E%202.1%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%0A%2F%2F%20Will%20print%0A%2F%2F2.0%3A%20x%20%3D%202%2C%20y%20%3D%202%0A%2F%2F--%3E%202.1%3A%20x%20%3D%201%2C%20y%20%3D%202%0A%0A%3B(()%20%3D%3E%20%7B%20%0A%20%20var%20x%2C%20y%20%3D%203%20%2F%2F%20%3D%3D%20var%20x%3B%20var%20y%20%3D%203%3B%0A%20%20console.log('3.0%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%7D)()%0Aconsole.log('--%3E%203.1%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%0A%2F%2F%20Will%20print%0A%2F%2F3.0%3A%20x%20%3D%20undefined%2C%20y%20%3D%203%0A%2F%2F--%3E%203.1%3A%20x%20%3D%201%2C%20y%20%3D%202%0A%0A%3B(()%20%3D%3E%20%7B%20%0A%20%20var%20y%2C%20x%20%3D%20y%20%3D%204%20%2F%2F%20%3D%3D%20var%20x%3B%20var%20y%3B%20x%20%3D%20y%20%3D%203%0A%20%20console.log('4.0%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%7D)()%0Aconsole.log('--%3E%204.1%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%0A%2F%2F%20Will%20print%0A%2F%2F4.0%3A%20x%20%3D%204%2C%20y%20%3D%204%0A%2F%2F--%3E%204.1%3A%20x%20%3D%201%2C%20y%20%3D%202%0A%0Ax%20%3D%205%20%2F%2F%20%3D%3D%20x%20%3D%205%0Aconsole.log('--%3E%205%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%0A%2F%2F%20Will%20print%0A%2F%2F--%3E%205%3A%20x%20%3D%205%2C%20y%20%3D%202)。

更多可用的資訊在 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)。

特別感謝 @kurtextrem 的合作 :)!
