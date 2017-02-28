---
layout: post

title: Paso de argumentos a las funciones de callback.
tip-number: 16
tip-username: minhazav
tip-username-profile: https://twitter.com/minhazav
tip-tldr: JavaScript modules and build steps are getting more numerous and complicated, but what about boilerplate in new frameworks? Modulos JavaScript y construir pasos son cada vez más numerosos y complicados, pero ¿qué pasa en nuevos frameworks?

redirect_from:
  - /es_es/passing-arguments-to-callback-functions/

categories:
    - es_ES
    - javascript
---

Por defecto no se puede pasar argumentos a una función de callback. Por ejemplo:

```js
function callback() {
  console.log('Hi human');
}

document.getElementById('someelem').addEventListener('click', callback);

```

You can take advantage of the closure scope in Javascript to pass arguments to callback functions. Check this example:
Puede aprovechar el closure scope en Javascript para pasar argumentos a funciones de callback. Compruebe este ejemplo:

```js
function callback(a, b) {
  return function() {
    console.log('sum = ', (a+b));
  }
}

var x = 1, y = 2;
document.getElementById('someelem').addEventListener('click', callback(x, y));

```

### Que son closures?

Closures son funciones que hacen referencia a las variables independientes (gratis). En otras palabras, la función definida en el closure "recuerda" el scope en el que se creó. [Check MDN Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) para conocer mas.


Así de esta manera los argumentos `x` y `y` están en el scope de la función de callback cuando se le llama.

Otro método para hacerlo es usando el método `bind`. Por ejemplo:

```js
var alertText = function(text) {
  alert(text);
};

document.getElementById('someelem').addEventListener('click', alertText.bind(this, 'hello'));
```
Hay una ligera diferencia en el rendimiento de ambos métodos, ver [jsperf](http://jsperf.com/bind-vs-closure-23).
