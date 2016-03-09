---
layout: post

title: Measure Operation time using console object
tip-number: xx
tip-username: SarjuHansaliya
tip-username-profile: https://github.com/SarjuHansaliya
tip-tldr: Measure Operation time using `console` object

categories:
    - en
---

Sometime we need to measure time of some tasks to analyze how much time it is taking to execute.To achieve that normal practice is to notedown time before starting of the task and notedown time after completion of the task , and then take a difference between two times.But that is lots of work for only time measuring.

Simple method is to do this thing is to use `console.time(label)` and `console.timeEnd(label)`.Here is the snippet.

```javascript
// `timer` is a label which will be used to end particular timer.
// Label can be any valid string.
console.time("timer"); 
YOUR_TASK();
console.timeEnd("timer");

//Output:: timer: x ms 
```
> Note : As [Mozilla](https://developer.mozilla.org/en-US/docs/Web/API/Console/time) suggested that don't use this for production sites , only use it for development purpose only.


