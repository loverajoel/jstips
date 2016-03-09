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

Sometime we need to measure time of some tasks to analyze how much time it takes to execute. To achieve that, normal practice is to note down time before starting the task and note down time after completing the task, and then take the difference between two times. But this is a lot of work for only time measuring.

The most simplest way to achieve this is to use `console.time(label)` and `console.timeEnd(label)`. Here is the snippet.

```javascript
// `timer` is a label which will be used to end that particular timer.
// Label can be any valid string.
console.time("timer"); 
YOUR_TASK();
console.timeEnd("timer");

//Output:: timer: x ms 
```
> Note : As [Mozilla](https://developer.mozilla.org/en-US/docs/Web/API/Console/time) suggested that don't use this for production sites, only use it for development purpose only.


