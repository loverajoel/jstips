---
layout: post

title: Dica para medir performance de um bloco de javascript
tip-number: 13
tip-username: manmadareddy
tip-username-profile: https://twitter.com/manmadareddy
tip-tldr: Para medir rapidamente a performance de um bloco de javascript, nós podemos usar as funções de console, como `console.time(label)` e `console.timeEnd(label)`

categories:
    - pt_BR
---

Para medir rapidamente a performance de um bloco de javascript, nós podemos usar as funções de console, como [`console.time(label)`](https://developer.chrome.com/devtools/docs/console-api#consoletimelabel) e [`console.timeEnd(label)`](https://developer.chrome.com/devtools/docs/console-api#consoletimeendlabel)

```javascript
console.time("Inicialização do array");
var arr = new Array(100),
    len = arr.length,
    i;

for (i = 0; i < len; i++) {
    arr[i] = new Object();
};
console.timeEnd("Inicialização do array"); // Saída: Inicialização do array: 0.711ms
```

Mais informações:
[Console object](https://github.com/DeveloperToolsWG/console-object),
[Javascript benchmarking](https://mathiasbynens.be/notes/javascript-benchmarking)

Demonstração: [jsfiddle](https://jsfiddle.net/meottb62/) - [codepen](http://codepen.io/anon/pen/JGJPoa) (saída no console do navegador)