---
 layout: post

title: How to check numbers (include zero)
tip-number: 16 (or anything else, idk)
tip-username: Danila Egorenko
tip-username-profile: https://t.me/danilaEgorenko, https://leetcode.com/danila_egorenko/
tip-tldr: Demo: https://onecompiler.com/javascript/3yv7nxpk7

 categories:
     - en
     - javascript
 ---

Hello, there!
Today I will show you how to define zero without ```typeof === 'number'``` and ```!== undefined```
Just write ```+ 1``` to variable, which you wanna check and enjoy it.
```
const elZero = 0
const elUndefined = undefined
console.log(elZero + 1) // 1 (true)
console.log(elUndefined + 1) // NaN (false)
```
It is very useful, when you use map, which contains zero in values.
```
const map = {1: 0, 2: undefined}
for (let el in map) {
  console.log(map[el] + 1)
  if (map[el] + 1) console.log(map[el]) // 0
}
```