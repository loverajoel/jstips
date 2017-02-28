---
layout: post

title: Improve Nested Conditionals
tip-number: 03
tip-username: AlbertoFuente 
tip-username-profile: https://github.com/AlbertoFuente
tip-tldr: How can we improve and make a more efficient nested `if` statement in javascript?

redirect_from:
  - /en/improve-nested-conditionals/

categories:
    - en
    - javascript
---

How can we improve and make a more efficient nested `if` statement in javascript?

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

One way to improve the nested `if` statement would be using the `switch` statement. Although it is less verbose and is more ordered, it's not recommended to use it because it's so difficult to debug errors. Here's [why](https://toddmotto.com/deprecating-the-switch-statement-for-object-literals).

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

But what if we have a conditional with several checks in each statement? In this case, if we want it less verbose and more ordered, we can use the conditional `switch`.
If we pass `true` as a parameter to the `switch` statement, it allows us to put a conditional in each case.

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

If refactoring is an option, we can try to simplify the functions themselves. For example instead of having a function for each background color we could have an function that takes the color as an argument.

```javascript
function printBackground(color) {
  if (!color || typeof color !== 'string') {
    return; // Invalid color, return immediately
  }
}
```

But if refactoring is not an option, we must always avoid having several checks in every condition and avoid using `switch` as much as possible. We also must take into account that the most efficient way to do this is through an `object`.

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

Here you can find more information about [this](http://www.nicoespeon.com/en/2015/01/oop-revisited-switch-in-js/).
