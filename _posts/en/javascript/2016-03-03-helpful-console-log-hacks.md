---
layout: post

title: Helpful Console Logging Tricks
tip-number: 50
tip-username: zackhall
tip-username-profile: https://twitter.com/zthall
tip-tldr: Helpful logging techniques using coercion and conditonal breakpoints.

redirect_from:
  - /en/helpful-console-log-hacks/

categories:
    - en
    - javascript
---

## Using conditional breakpoints to log data

If you wanted to log to the console a value each time a function is called, you can use conditional break points to do this. Open up your dev tools, find the function where you'd like to log data to the console and set a breakpoint with the following condition:

```js
console.log(data.value) && false
```

A conditional breakpoint pauses the page thread only if the condition for the breakpoint evaluates to true. So by using a condition like console.log('foo') && false it's guaranteed to evaluate to false since you're putting the literal false in the AND condition. So this will not pause the page thread when it's hit, but it will log data to the console. This can also be used to count how many times a function or callback is called.

Here's how you can set a conditional breakpoint in [Edge](https://dev.windows.com/en-us/microsoft-edge/platform/documentation/f12-devtools-guide/debugger/#setting-and-managing-breakpoints "Managing Breakpoints in Edge"), [Chrome](https://developer.chrome.com/devtools/docs/javascript-debugging#breakpoints "Managing Breakpoints in Chrome"), [Firefox](https://developer.mozilla.org/en-US/docs/Tools/Debugger/How_to/Set_a_conditional_breakpoint "Managing Breakpoints in Firefox") and [Safari](https://developer.apple.com/library/mac/documentation/AppleApplications/Conceptual/Safari_Developer_Guide/Debugger/Debugger.html "Managing Breakpoints in Safari").

## Printing a function variable to console

Have you ever logged a function variable to the console and weren't able to just view the function's code? The quickest way to see the function's code is to coerce it to a string using concatenation with an empty string.

```js
console.log(funcVariable + '');
```