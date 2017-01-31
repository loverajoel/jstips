---
layout: post

title: Улучшаем вложенные условия
tip-number: 03
tip-username: AlbertoFuente
tip-username-profile: https://github.com/AlbertoFuente
tip-tldr: Как мы можем улучшить и сделать более эффективными вложенные условные выражения в javascript?

categories:
    - ru_RU
---

Как мы можем улучшить и сделать более эффективными вложенные условные выражения в javascript?

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

Один из способов улучшения вложенных условных выражений — использование конструкции `switch`. Несмотря на то, что она менее объемна и более структурирована, не рекомендуется её использовать из-за сложности отладки ошибок. Вот [почему](https://toddmotto.com/deprecating-the-switch-statement-for-object-literals)

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

Но что если у нас условие с несколькими проверками? В этом случае, если мы хотим меньше кода и больше структурированности, можем использовать `switch`.
Если передать `true` как параметр в `switch`, мы сможем использовать условие в каждом случае.

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

Если есть возможность сделать рефакторинг, мы можем упростить код. Например, вместо того, чтобы держать для каждого фонового цвета свою функцию, у будет одна функция, которая принимает цвет как аргумент.

```javascript
function printBackground(color) {
  if (!color || typeof color !== 'string') {
    return; // Color невалиден, прекращаем работу функции
  }
}
```

Если возможности рефакторинг сделать нет, мы должны избегать нескольких проверок на каждое условие и по возможности избегать использование `switch`. И наиболее эффективный способ в данном случае — использование объекта.

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

Больше информации про это вы можете найти [здесь](http://www.nicoespeon.com/en/2015/01/oop-revisited-switch-in-js/).
