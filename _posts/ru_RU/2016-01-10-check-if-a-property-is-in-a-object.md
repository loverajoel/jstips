---
layout: post

title: Проверяем наличие свойства в объекте
tip-number: 10
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: Способы проверки наличия свойств в объекте.
tip-writer-support: https://www.coinbase.com/loverajoel

categories:
    - ru_RU
---

Когда вам надо проверить есть ли у [объекта](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects) свойство, вы вероятно пишете что-то вроде этого:

```javascript
var myObject = {
  name: '@tips_js'
};

if (myObject.name) { ... }

```

Это нормальный вариант, но вам также стоит знать, что есть 2 встроенных способа сделать подобное, [оператор `in`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in) и [`Object.hasOwnProperty`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty). Любой объект наследуемый от `Object`, имеет эти методы.

### Различия в работе

```javascript
var myObject = {
  name: '@tips_js'
};

myObject.hasOwnProperty('name'); // true
'name' in myObject; // true

myObject.hasOwnProperty('valueOf'); // false, valueOf унаследован по цепочке прототипов
'valueOf' in myObject; // true

```

Они отличаются глубиной проверки свойств. Другими словами `hasOwnProperty` вернет истину, если ключ содержится в объекте. Тогда как оператор `in` не различает свойства самого объекта и свойства, которые наследуются от прототипа.

Вот другой пример:

```javascript
var myFunc = function() {
  this.name = '@tips_js';
};
myFunc.prototype.age = '10 days';

var user = new myFunc();

user.hasOwnProperty('name'); // true
user.hasOwnProperty('age'); // false, потому что age наследуется из цепочки прототипов
```

Больше [примеров](https://jsbin.com/tecoqa/edit?js,console)!

Я также рекоменду прочитать [эту дискуссию](https://github.com/loverajoel/jstips/issues/62) про распространненые ошибки при проверке наличия свойств в объектах.
