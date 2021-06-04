---
layout: post

titolo: Consiglio per misurare le prestazioni di un blocco di codice javascript
tip-numero: 13
tip-username: manmadareddy
tip-username-profile: https://twitter.com/manmadareddy
tip-tldr: Per misurare velocemente le prestazioni di un blocco di codice javascript, possiamo utilizzare le funzioni console come `console.time(label)` e `console.timeEnd(label)`

categoria:
    - it
---

Per misurare velocemente le prestazioni di un blocco di codice javascript, possiamo utilizzare le funzioni console come
[`console.time(label)`](https://developer.chrome.com/devtools/docs/console-api#consoletimelabel) e [`console.timeEnd(label)`](https://developer.chrome.com/devtools/docs/console-api#consoletimeendlabel)

```javascript
console.time("Array initialize");
var arr = new Array(100),
    len = arr.length,
    i;

for (i = 0; i < len; i++) {
    arr[i] = new Object();
};
console.timeEnd("Array initialize"); // Restituisce: Array initialize: 0.711ms
```

Per maggiori informazioni:
[Console object](https://github.com/DeveloperToolsWG/console-object),
[Javascript benchmarking](https://mathiasbynens.be/notes/javascript-benchmarking)

Demo: [jsfiddle](https://jsfiddle.net/meottb62/) - [codepen](http://codepen.io/anon/pen/JGJPoa) (outputs in browser console)
