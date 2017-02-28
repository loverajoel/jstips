---
layout: post

title: Tip para medir el rendimiento de un bloque de Javascript
tip-number: 13
tip-username: manmadareddy
tip-username-profile: https://twitter.com/manmadareddy
tip-tldr: Para medir rápidamente el rendimiento de un bloque de Javascript, podemos utilizar las funciones de la consola como `console.time(label)` y `console.timeEnd(label)`

redirect_from:
  - /es_es/tip-to-measure-performance-of-a-javascript-block/

categories:
    - es_ES
    - javascript
---

Para medir rápidamente el rendimiento de un bloque de Javascript, podemos utilizar las funciones de la consola como
[`console.time(label)`](https://developer.chrome.com/devtools/docs/console-api#consoletimelabel) y [`console.timeEnd(label)`](https://developer.chrome.com/devtools/docs/console-api#consoletimeendlabel)

```javascript
console.time("Array initialize");
var arr = new Array(100),
    len = arr.length,
    i;

for (i = 0; i < len; i++) {
    arr[i] = new Object();
};
console.timeEnd("Array initialize"); // Outputs: Array initialize: 0.711ms
```

Más informacion:
[Console object](https://github.com/DeveloperToolsWG/console-object),
[Javascript benchmarking](https://mathiasbynens.be/notes/javascript-benchmarking)

Demo: [jsfiddle](https://jsfiddle.net/meottb62/) - [codepen](http://codepen.io/anon/pen/JGJPoa) (outputs in browser console)