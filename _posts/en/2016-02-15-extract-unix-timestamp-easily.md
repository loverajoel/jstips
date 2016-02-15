---
layout: *post

title: Easiest way to extract unix timestamp in JS
tip-number: 15
tip-username: nmrony
tip-username-profile: https://github.com/nmrony
tip-tldr: In Javascript you can easily get the unix timestamp

categories:
    - en
---

We frequently need to calculate with unix timestamp. I think this is the most easiest way to grab the unix timestamp in Javascript. You just need to add a `+` sign when declaring a `Date` object like below

```js
const timestamp = +new Date()
```
To get unix timestamp of a specific date pass `yyyy-mm-dd` as a parameter of `Date` constructor. For example
```js
const timestamp = +new Date('2012-06-08')
```