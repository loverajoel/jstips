---
layout: post

title: Mejorar anidaciones Condicionales
tip-number: 03
tip-username: AlbertoFuente 
tip-username-profile: https://github.com/AlbertoFuente
tip-tldr: ¿Cómo podemos mejorar y hacer una declaración anidada `if` más eficiente en javascript?

redirect_from:
  - /es_es/improve-nested-conditionals/

categories:
    - es_ES
    - javascript
---

¿Cómo podemos mejorar y hacer una declaración anidada `if` más eficiente en javascript?

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

Una forma de mejorar el `if` anidado sería usar `switch`. Aunque es menos verbosa y está más ordenado, no se recomienda su uso porque es muy difícil de depurar errores. Aquí [por eso] (https://toddmotto.com/deprecating-the-switch-statement-for-object-literals/).

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

Pero lo que si tenemos un condicional con varios controles en cada declaración? en este caso, si queremos que sean menos detalladas y más ordenada, podemos utilizar el condicional `switch`.
Si pasamos `true` como parámetro a la declaración `switch`, que nos permite colocar un condicional en cada caso.

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

Pero siempre hay que evitar tener varios controles en todas las condiciones y evitar el uso de `switch` tanto como sea posible. También hay que tener en cuenta que la forma más eficiente de hacer esto es a través de un `object`.

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

Aqui puede obtener mas informacion [this](http://www.nicoespeon.com/en/2015/01/oop-revisited-switch-in-js/).
