---
layout: post

title: Преобразуем NodeList в массив
tip-number: 08
tip-username: Tevko
tip-username-profile: https://twitter.com/tevko
tip-tldr: Быстрый, безопасный и переиспользуемый способ превратить NodeList в массив DOM-элементов

categories:
    - ru_RU
---

Метод `querySelectorAll` возвращает объект подобный массиву, который называется NodeList (список узлов). Эти структуры данных называются массивоподобными, потому что они выглядят как массивы, но к ним нельзя применить такие методы, как `map` или `forEach`. Быстрый, безопасный и переиспользуемый способ превратить NodeList в массив DOM-элементов:

```javascript
const nodelist = document.querySelectorAll('div');
const nodelistToArray = Array.apply(null, nodelist);

//после этого ..

nodelistToArray.forEach(...);
nodelistToArray.map(...);
nodelistToArray.slice(...);

//и так далее...
```

Метод `apply` используется для передачи массива аргументов в функцию с указанием значения `this`. [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) сообщает, что `apply` принимает массивоподобный объект, как раз то, что возвращает `querySelectorAll`. Поскольку нам не надо указывать значение `this` в контексте функции, мы передаем `null` или `0`. В результате мы получим массив DOM-элементов, который имеет все методы массива.

Альтернативный вариант — использование `Array.prototype.slice` в связке с `Function.prototype.call` или `Function.prototype.apply` с передачей массивоподобного объекта в качестве значения `this`:

```javascript
const nodelist = document.querySelectorAll('div');
const nodelistToArray = Array.prototype.slice.call(nodelist); // или эквивалент Array.prototype.slice.apply(nodelist);

//после этого ..

nodelistToArray.forEach(...);
nodelistToArray.map(...);
nodelistToArray.slice(...);

//и так далее...
```

Если вы пишете на ES2015, вы можете использовать [оператор "spread" `...`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)

```js
const nodelist = [...document.querySelectorAll('div')]; // возвращает настоящий массив

//после этого ..

nodelist.forEach(...);
nodelist.map(...);
nodelist.slice(...);

//и так далее...
```
