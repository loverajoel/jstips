---
layout: default
title: "Tip to measure performance of a javascript block"
author: "@manmadareddy"
author-link: https://twitter.com/manmadareddy
---

For quickly measuring performance of a javascript block, we can use the console functions like
[```console.time(label)```](https://developer.chrome.com/devtools/docs/console-api#consoletimelabel) and [```console.timeEnd(label)```](https://developer.chrome.com/devtools/docs/console-api#consoletimeendlabel)

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

More info:
[Console object](https://github.com/DeveloperToolsWG/console-object),
[Javascript benchmarking](https://mathiasbynens.be/notes/javascript-benchmarking)

Demo: [jsfiddle](https://jsfiddle.net/meottb62/) - [codepen](http://codepen.io/anon/pen/JGJPoa) (outputs in browser console)
