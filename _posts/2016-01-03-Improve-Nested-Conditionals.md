---
layout: default
title: "Improve Nested Conditionals"
author: "AlbertoFuente"
author-link: https://github.com/AlbertoFuente
---

How can we improve and make more efficient nested `if` statement in javascript.

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

One way to improve the nested `if` statement would be using the `switch` statement. Although it is less verbose and is more ordered, It's not recommended to use it because it's so difficult to debug errors, here's [why](https://toddmotto.com/deprecating-the-switch-statement-for-object-literals/).

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

But what if we have a conditional with several checks in each statement? In this case, if we like to do less verbose and more ordered, we can use the conditional `switch`.
If we pass `true` as parameter to the `switch` statement, It allows us to put a conditional in each case.

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

But we must always avoid having several checks in every condition, avoiding use of `switch` as far as possible and take into account that the most efficient way to do this is through an `object`.

```javascript
var colorObj = {
  'black': printBlackBackground,
  'red': printRedBackground,
  'blue': printBlueBackground,
  'green': printGreenBackground,
  'yellow': printYellowBackground
};

if (color && colorObj.hasOwnProperty(color)) {
  colorObj[color]();
}
```

Here you can find more information about [this](http://www.nicoespeon.com/en/2015/01/oop-revisited-switch-in-js/).
