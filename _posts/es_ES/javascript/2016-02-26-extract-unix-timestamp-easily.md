---
layout: post

title: La manera más fácil de extraer marca de tiempo Unix en JS
tip-number: 49
tip-username: nmrony
tip-username-profile: https://github.com/nmrony
tip-tldr: En Javascript se puede conseguir fácilmente la marca de tiempo Unix

redirect_from:
  - /es_es/extract-unix-timestamp-easily/
  
categories:
    - es_ES
    - javascript
---

Con frecuencia tenemos que calcular con marca de tiempo unix. Hay varias maneras de agarrar la marca de tiempo. La forma mas rapida y facil es

```js
const dateTime = Date.now();
const timestamp = Math.floor(dateTime / 1000);
```
or

```js
const dateTime = new Date().getTime();
const timestamp = Math.floor(dateTime / 1000);
```

Para conseguir marca de tiempo unix de una fecha específica pasar `YYYY-MM-DD` o `YYYY-MM-DDT00:00:00Z` como parámetro del constructor `Date`. Por ejemplo

```js
const dateTime = new Date('2012-06-08').getTime();
const timestamp = Math.floor(dateTime / 1000);
```
Usted puede añadir un signo `+` también cuando se declara un objeto `Date`, como a continuación

```js
const dateTime = +new Date();
const timestamp = Math.floor(dateTime / 1000);
```
o para una fecha especifica

```js
const dateTime = +new Date('2012-06-08');
const timestamp = Math.floor(dateTime / 1000);
```

Bajo el capó la ejecucion de llamadas del metodo `valueOf` del objeto `Date`. A continuación, el unario `+` operador llama `toNumber()` con ese valor devuelto. Para una explicación más detallada, consultar los siguientes enlaces

* [Date.prototype.valueOf](http://es5.github.io/#x15.9.5.8)
* [Unary + operator](http://es5.github.io/#x11.4.6)
* [toNumber()](http://es5.github.io/#x9.3)
* [Date Javascript MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
* [Date.parse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/parse)
