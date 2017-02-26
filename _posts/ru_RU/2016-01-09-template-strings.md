---
layout: post

title: Шаблонные строки
tip-number: 09
tip-username: JakeRawr
tip-username-profile: https://github.com/JakeRawr
tip-tldr: В ES6, JS получил строки-шаблоны как альтернативу классическим строкам с кавычками.

categories:
    - ru_RU
---

В ES6, JS получил шаблонные строки как альтернативу классическим строкам с кавычками.

Примеры:
Обычная строка

```javascript
var firstName = 'Jake';
var lastName = 'Rawr';
console.log('My name is ' + firstName + ' ' + lastName);
// My name is Jake Rawr
```
Строка-шаблон

```javascript
var firstName = 'Jake';
var lastName = 'Rawr';
console.log(`My name is ${firstName} ${lastName}`);
// My name is Jake Rawr
```

Вы можете вводить многострочный текст без использования символа `\n`, делать простые сложения (например, 2+3) и даже использовать [тернарный оператор](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) внутри `${}` в шаблонных строках.

```javascript
var val1 = 1, val2 = 2;
console.log(`${val1} is ${val1 < val2 ? 'less than': 'greater than'} ${val2}`)
// 1 is less than 2
```

Вы также можете изменять вывод шаблонных строк, используя функцию; они называются [тегированными шаблонными строками](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings#Tagged_template_strings).

[Здесь](https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2) вы можете прочитать больше информации о шаблонных строках.
