---
layout: post

title: 优化嵌套的条件语句
tip-number: 03
tip-username: AlbertoFuente 
tip-username-profile: https://github.com/AlbertoFuente
tip-tldr: 我们怎样来提高和优化javascript里嵌套的`if`语句呢？

categories:
    - zh_CN
---


我们怎样来提高和优化javascript里嵌套的`if`语句呢？

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


一种方法来提高嵌套的`if`语句是用`switch`语句。虽然它不那么啰嗦而且排列整齐，但是并不建议使用它，因为这对于调试错误很困难。这告诉你[为什么](https://toddmotto.com/deprecating-the-switch-statement-for-object-literals).

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


但是如果在每个语句中都有很多条件检查时该怎么办呢？这种情况下，如果我们想要不罗嗦又整洁的话，我们可以用有条件的`switch`。如果我们传递`true`给`switch`语句，我们便可以在每个case中使用条件语句了。

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


但是我们应该时刻注意避免太多判断在一个条件里，尽量少的使用`switch`，考虑最有效率的方法：借助`object`。

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


这里有更多相关的[内容](http://www.nicoespeon.com/en/2015/01/oop-revisited-switch-in-js/).

