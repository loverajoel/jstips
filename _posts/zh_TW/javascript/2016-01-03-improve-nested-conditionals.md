---
layout: post

title: 改善巢狀化的條件式
tip-number: 03
tip-username: AlbertoFuente
tip-username-profile: https://github.com/AlbertoFuente
tip-tldr: 我們要如何在 JavaScript 改善巢狀化的 `if` 條件式？

redirect_from:
  - o/zh_tw/improve-nested-conditionals/

categories:
    - zh_TW
    - javascript
---

我們要如何在 JavaScript 改善巢狀化的 `if` 條件式？

```javascript
if (color) {
  if (color === 'black') {
    printBlackBackground();
  } else if (color === 'red') {
    printRedBackground();
  } else if (color === 'blue') {
    printBlueBackground();
  } else if (color === 'green') {
    printGreenBackground();
  } else {
    printYellowBackground();
  }
}
```

有一種方式可以改善巢狀化的 `if` 條件式是使用 `switch` 陳述式。雖然更簡潔有序，但是不建議使用，因為它不容易 debug 錯誤。告訴你[為什麼](https://toddmotto.com/deprecating-the-switch-statement-for-object-literals)。

```javascript
switch(color) {
  case 'black':
    printBlackBackground();
    break;
  case 'red':
    printRedBackground();
    break;
  case 'blue':
    printBlueBackground();
    break;
  case 'green':
    printGreenBackground();
    break;
  default:
    printYellowBackground();
}
```

但是，如果我們語句中都有很多條件檢查呢？在這個情況下，如果我們想要讓它更簡潔有序，我們可以使用有條件的 `switch`。
如果我們傳送 `true` 當作參數給 `switch` 陳述式，允許我們在每個 case 下使用條件式。

```javascript
switch(true) {
  case (typeof color === 'string' && color === 'black'):
    printBlackBackground();
    break;
  case (typeof color === 'string' && color === 'red'):
    printRedBackground();
    break;
  case (typeof color === 'string' && color === 'blue'):
    printBlueBackground();
    break;
  case (typeof color === 'string' && color === 'green'):
    printGreenBackground();
    break;
  case (typeof color === 'string' && color === 'yellow'):
    printYellowBackground();
    break;
}
```

如果重構是一個選擇的話，我們可以嘗試的簡化這些函式。例如，不需要為每個顏色寫一個函式，我們可以寫一個以顏色作為參數的函式。

```javascript
function printBackground(color) {
  if (!color || typeof color !== 'string') {
    return; // 不正確的顏色，立即返回
  }
}
```

如果重構不是一個選擇的話，我們必須避免使用過多的條件檢查以及避免使用 switch。我們使用最有效率的方式，透過 object。

```javascript
var colorObj = {
  'black': printBlackBackground,
  'red': printRedBackground,
  'blue': printBlueBackground,
  'green': printGreenBackground,
  'yellow': printYellowBackground
};

if (color in colorObj) {
  colorObj[color]();
}
```

這裡你可以找到更多的資訊關於 [switch](http://www.nicoespeon.com/en/2015/01/oop-revisited-switch-in-js/)。
