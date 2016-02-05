---
layout: post

title: Melhorar Condicionais Aninhados
tip-number: 03
tip-username: AlbertoFuente 
tip-username-profile: https://github.com/AlbertoFuente
tip-tldr: Como podemos melhorar e tornar mais eficiente a declaração de `if` aninhados em javascript?

categories:
    - pt_BR
---

Como podemos melhorar e tornar mais eficiente a declaração de `if` aninhados em javascript?

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

Uma forma de melhorar declarações de `if` aninhados seria usar `switch`. Embora seja menos verboso e mais ordenado, o uso não é recomendado porque seu debug é muito difícil. [Aqui](https://toddmotto.com/deprecating-the-switch-statement-for-object-literals) o porquê.

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

Mas e se tivermos uma condicional com várias avaliações em cada declaração? Nesse caso, se quisermos algo menos verboso e mais ordenado, podemos usar o condicional `switch`.
Se passarmos `true` como um parâmetro para o `switch`, ele nos permitirá usar uma condicional em cada caso.

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

Mas devemos sempre evitar muitas verificações em cada condição e evitar `switch` sempre que possível. Também devemos levar em conta que a forma mais eficiente de fazer isto é usando um `object`.

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

[Aqui](http://www.nicoespeon.com/en/2015/01/oop-revisited-switch-in-js/) você pode encontrar mais informações sobre isto.
