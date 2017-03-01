---
layout: post

title: Averiguar si una propiedad está en un Objeto
tip-number: 10
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: Estas son formas de comprobar si una propiedad está presente en un objeto.
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /es_es/check-if-a-property-is-in-a-object/

categories:
    - es_ES
    - javascript
---

Cuando usted tiene que comprobar si una propiedad está presente en un [object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects), es probable que esté haciendo algo como esto:

```javascript
var myObject = {
  name: '@tips_js'
};

if (myObject.name) { ... }

```
Eso está bien, pero hay que saber que existen dos formas nativas para este tipo de cosas, el [`in` operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in) y [`Object.hasOwnProperty`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty). Cada objeto descendiente de `Object`.

### Observe esta gran diferencia

```javascript
var myObject = {
  name: '@tips_js'
};

myObject.hasOwnProperty('name'); // true
'name' in myObject; // true

myObject.hasOwnProperty('valueOf'); // false, valueOf is inherited from the prototype chain
'valueOf' in myObject; // true

```

Ambos difieren en la profundidad a la que se comprueban las propiedades. En otras palabras, `hasOwnProperty` sólo devolverá verdadero si la clave está disponible en ese objeto directamente. Sin embargo, el operador `in` no discrimina entre las propiedades creadas en un objeto y las propiedades heredadas de la cadena de prototipo.

Aqui otro ejemplo:

```javascript
var myFunc = function() {
  this.name = '@tips_js';
};
myFunc.prototype.age = '10 days';

var user = new myFunc();

user.hasOwnProperty('name'); // true
user.hasOwnProperty('age'); // false, because age is from the prototype chain
```

Mire este link [live examples here](https://jsbin.com/tecoqa/edit?js,console)!

Recomiendo que lean [this discussion](https://github.com/loverajoel/jstips/issues/62) acerca de los errores comunes el momento del control de la existencia de una propiedad en objetos.