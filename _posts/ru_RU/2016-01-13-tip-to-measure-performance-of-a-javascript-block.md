---
layout: post

title: Измеряем производительность куска кода
tip-number: 13
tip-username: manmadareddy
tip-username-profile: https://twitter.com/manmadareddy
tip-tldr: Для быстрого измерения производительности куска кода в javascript, мы можем использовать функции консоли `console.time(label)` и `console.timeEnd(label)`

categories:
    - ru_RU
---

Для быстрого измерения производительности куска кода в javascript, мы можем использовать функции консоли
[`console.time(label)`](https://developer.chrome.com/devtools/docs/console-api#consoletimelabel) и [`console.timeEnd(label)`](https://developer.chrome.com/devtools/docs/console-api#consoletimeendlabel)

```javascript
console.time("Создание массива");
var arr = new Array(100),
    len = arr.length,
    i;

for (i = 0; i < len; i++) {
    arr[i] = new Object();
};
console.timeEnd("Array initialize"); // Выведет: Создание массива: 0.711ms
```

Больше информации:
[Объект console](https://github.com/DeveloperToolsWG/console-object),
[Javascript бенчмаркинг](https://mathiasbynens.be/notes/javascript-benchmarking)

Демо: [jsfiddle](https://jsfiddle.net/meottb62/) - [codepen](http://codepen.io/anon/pen/JGJPoa) (выводит результат в браузерной консоли)

> Заметка: Как заметила [Mozilla](https://developer.mozilla.org/en-US/docs/Web/API/Console/time), используйте этот подход только в процессе разработки, не на работающих сайтах.
