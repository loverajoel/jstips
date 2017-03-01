---
layout: post

title: 实用的`log`技巧
tip-number: 50
tip-username: zackhall
tip-username-profile: https://twitter.com/zthall
tip-tldr: 运用`&&`与条件断点的实用的`log`技巧

redirect_from:
  - /zh_cn/helpful-console-log-hacks/

categories:
    - zh_CN
    - javascript
---

## 使用条件断点输出`log`

如果你想当函数每次被调用时都在控制台打印一个值，你可以应用条件断点来实现。打开你的开发工具，找到你准备打印的值所在的函数然后使用如下条件设置一个条件断点：

```js
console.log(data.value) && false
```

条件断点只有在条件运行的结果为`true`时才会中断页面。所以使用`console.log('foo') && false`这样的条件，由于你把`false`放在了`AND`条件中，所以结果肯定是`false`。因此这并不会中断页面但是会打印`log`到控制台。这也可以应用在计算某个函数或回调被调用了多少次上面。

这里有各个平台下设置条件断点的方法：[Edge](https://dev.windows.com/en-us/microsoft-edge/platform/documentation/f12-devtools-guide/debugger/#setting-and-managing-breakpoints "Managing Breakpoints in Edge")、[Chrome](https://developer.chrome.com/devtools/docs/javascript-debugging#breakpoints "Managing Breakpoints in Chrome")、[Firefox](https://developer.mozilla.org/en-US/docs/Tools/Debugger/How_to/Set_a_conditional_breakpoint "Managing Breakpoints in Firefox")、[Safari](https://developer.apple.com/library/mac/documentation/AppleApplications/Conceptual/Safari_Developer_Guide/Debugger/Debugger.html "Managing Breakpoints in Safari")。

## 打印函数到控制台

你曾经有过打算打印函数到控制台却不能看到函数的代码的情况吗？最快的方法查看函数的代码是将其与空字符串连接，从而将其强制转换为字符串。

```js
console.log(funcVariable + '');
```