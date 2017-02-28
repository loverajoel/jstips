---
layout: post

title: Evitar la modificación o pasando `arguments` en otras funciones - mata la optimización

tip-number: 31
tip-username: berkana
tip-username-profile: https://github.com/berkana
tip-tldr: Dentro de las funciones de JavaScript, el nombre de la variable `arguments` le permite acceder a todos los argumentos pasados a la función. `arguments` en un *array-like object*; `arguments` se puede acceder usando array notation, y tiene la propiedad *longitud*, pero no tiene muchos de los métodos incorporados en arrays que tienen como `filter` y `map` y `forEach`. Debido a esto, es una práctica bastante común para convertir `arguments` en una matriz utilizando el siguiente fragmento.


redirect_from:
  - /es_es/avoid-modifying-or-passing-arguments-into-other-functions-it-kills-optimization/

categories:
    - es_ES
    - javascript
---

###Background

Dentro de las funciones de JavaScript, el nombre de la variable [`arguments`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments) le permite acceder a todos los argumentos pasados a la función. `arguments` es una *array-like object*; `arguments` se puede acceder usando la array notation, y tiene la propiedad *longitud*, pero no tiene por qué muchos de los métodos incorporados en los arrays que tienen como`filter` y `map` y `foreach`. Debido a esto, es una práctica bastante común para convertir `arguments` en un array utilizando:

```js
var args = Array.prototype.slice.call(arguments);
```
Este método `slice` del prototipo `array`, pasándole `arguments`; el método `slice` devuelve una copia superficial del `arguments` como un nuevo objeto de matriz. A la abreviatura común para esto es:

```js
var args = [].slice.call(arguments);
```
En este caso, en lugar de llamar `slice` del prototipo `Array`, se trata simplemente de ser llamado desde un array vacío literal.

###Optimización

Desafortunadamente, pasando `arguments` en cualquier llamada de función hará que el motor V8 JavaScript utilizado en Chrome y NodeJS para omitir la optimización de la función que hace esto, lo que puede resultar en un rendimiento considerablemente más lento. Ver este artículo [optimization killers](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers). Pasando `arguments` a cualquier otra función que se conoce como *leaking `arguments`*.

En cambio, si quieres un array de los argumentos que le permite utilizar lo que necesita recurrir a este:

```js
var args = new Array(arguments.length);
for(var i = 0; i < args.length; ++i) {
  args[i] = arguments[i];
}
```

Sí, es más prolija, pero en el código de producción, vale la pena para la optimización del rendimiento.