---
layout: post

title: Tip to measure performance of a javascript block
tip-number: 13
tip-username: manmadareddy
tip-username-profile: https://twitter.com/manmadareddy
tip-tldr: For quickly measuring performance of a javascript block, we can use the console functions like `console.time(label)` and `console.timeEnd(label)`

redirect_from:
  - /en/tip-to-measure-performance-of-a-javascript-block/

categories:
    - en
    - javascript
---

For quickly measuring performance of a javascript block, we can use the console functions like
[`console.time(label)`](https://developer.chrome.com/devtools/docs/console-api#consoletimelabel) and [`console.timeEnd(label)`](https://developer.chrome.com/devtools/docs/console-api#consoletimeendlabel)

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

> Note: As [Mozilla](https://developer.mozilla.org/en-US/docs/Web/API/Console/time) suggested don't use this for production sites, use it for development purposes only.