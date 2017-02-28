---
layout: post

title:  测量javascript代码块性能的小知识
tip-number: 13
tip-username: manmadareddy
tip-username-profile: https://twitter.com/manmadareddy
tip-tldr: 快速的测量javascript的性能，我们可以使用console的方法，例如 ```console.time(label)```和 ```console.timeEnd(label)```

redirect_from:
  - /zh_cn/fat-arrow-functions/

categories:
    - zh_CN
    - javascript
---

快速的测量javascript的性能，我们可以使用console的方法，例如
[```console.time(label)```](https://developer.chrome.com/devtools/docs/console-api#consoletimelabel) 和 [```console.timeEnd(label)```](https://developer.chrome.com/devtools/docs/console-api#consoletimeendlabel)


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


更多内容:
[Console object](https://github.com/DeveloperToolsWG/console-object),
[Javascript benchmarking](https://mathiasbynens.be/notes/javascript-benchmarking)

Demo: [jsfiddle](https://jsfiddle.net/meottb62/) - [codepen](http://codepen.io/anon/pen/JGJPoa) (在浏览器控制台输出)

> 注意：由于[Mozilla](https://developer.mozilla.org/zh-CN/docs/Web/API/Console/time)不建议将其使用在线上项目中，建议仅在开发中使用。