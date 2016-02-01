---
layout: post

title: 향상된 Nested Conditionals(중첩조건문)
tip-number: 03
tip-username: AlbertoFuente 
tip-username-profile: https://github.com/AlbertoFuente
tip-tldr: 어떻게 해야 자바스크립트에서 더 향상되고 효율적인 `if` 선언문을 만들 수 있을까?

categories:
    - ko
---
<translator: https://github.com/tisohjung>

어떻게 해야 자바스크립트에서 더 향상되고 효율적인 `if` 선언문을 만들 수 있을까?

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

`if`문을 향상시키는 방법중 하나는 `switch`문을 사용하는 것이다. 더 간결하고 순차적으로 보이지만 디버깅과 에러를 찾는데 있어서 어렵기 때문에 권장하진 않았다. [그 이유는 여기에 나와있다](https://toddmotto.com/deprecating-the-switch-statement-for-object-literals/).

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

하지만 각각의 조건에 몇가지 검사가있다면? 여기서 덜 간결하지만 순차적인 표현을 원한다면 조건적 `switch`문을 사용하면된다.
`switch`문에 `true`값만 넘기면 각각의 케이스에 조건문을 넣을 수 있다.

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

그래도 역시 최대한 각각의 조건문의 검사와 `switch`문 사용을 자제 해야한다. 그리고 가장 좋은 방법은 `object`를 사용하는 것임을 고려해야한다.

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

[이것에 대한 정보는 여기서 더 찾을 수 있다.](http://www.nicoespeon.com/en/2015/01/oop-revisited-switch-in-js/)
