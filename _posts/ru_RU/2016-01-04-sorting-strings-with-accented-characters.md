---
layout: post

title: Сортировка строк с акцентированными символами
tip-number: 04
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: В JavaScript есть метод **sort**, сортирующий массивы. Простой вызов `array.sort()` преобразует все элементы массива в строки и отсортирует их в алвафитном порядке. Если вы попробуете упорядочить массив из не ASCII символов, вы получите неожиданный результат.
tip-writer-support: https://www.coinbase.com/loverajoel

categories:
    - ru_RU
---

В JavaScript есть метод **[sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)**, сортирующий массивы. Простой вызов `array.sort()` преобразует все элементы массива в строки и отсортирует их в алвафитном порядке. У нас также возможность передать свою [логику сортировки](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort#Parameters) в метод.

```javascript
['Shanghai', 'New York', 'Mumbai', 'Buenos Aires'].sort();
// ["Buenos Aires", "Mumbai", "New York", "Shanghai"]
```

Если вы попробуете упорядочить массив из не ASCII символов `['é', 'a', 'ú', 'c']`, вы получите странный результат `['c', 'e', 'á', 'ú']`. Это происходит из-за того, что сортировка работает только с английским языком.

Взгляните на следующий пример:

```javascript
// Spanish
['único','árbol', 'cosas', 'fútbol'].sort();
// ["cosas", "fútbol", "árbol", "único"] // неправильный порядок

// German
['Woche', 'wöchentlich', 'wäre', 'Wann'].sort();
// ["Wann", "Woche", "wäre", "wöchentlich"] // неправильный порядок
```

К счастью, есть 2 способа изменить это поведение
[localeCompare](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare) и
[Intl.Collator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Collator) представленные спецификацией ECMAScript Internationalization API.

> У этих методов есть свои параметры для конфигурации правильной работы.

### Использование `localeCompare()`

```javascript
['único','árbol', 'cosas', 'fútbol'].sort(function (a, b) {
  return a.localeCompare(b);
});
// ["árbol", "cosas", "fútbol", "único"]

['Woche', 'wöchentlich', 'wäre', 'Wann'].sort(function (a, b) {
  return a.localeCompare(b);
});
// ["Wann", "wäre", "Woche", "wöchentlich"]
```

### Использование `Intl.Collator()`

```javascript
['único','árbol', 'cosas', 'fútbol'].sort(Intl.Collator().compare);
// ["árbol", "cosas", "fútbol", "único"]

['Woche', 'wöchentlich', 'wäre', 'Wann'].sort(Intl.Collator().compare);
// ["Wann", "wäre", "Woche", "wöchentlich"]
```

- У каждого метода вы можете настроить локаль.
- Согласно [Firefox](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare#Performance) Intl.Collator быстрее при сравнивании большого количества строк.

И так, когда вы работаете с массивом строк на языке отличном от Английского, используйте эти методы, чтобы избежать неожиданной сортировки.
