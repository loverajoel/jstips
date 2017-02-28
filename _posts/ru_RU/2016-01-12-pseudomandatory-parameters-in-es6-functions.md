---
layout: post

title: Псевдообязательные параметры в ES2015 функциях
tip-number: 12
tip-username: Avraam Mavridis
tip-username-profile: https://github.com/AvraamMavridis
tip-tldr: Во многих языка программирования параметры функции по умолчанию обязательны и разработчик должен отдельно указать, если параметр опционален.

categories:
    - ru_RU
---

Во многих языка программирования параметры функции по умолчанию обязательны и разработчик должен отдельно указать, если параметр опционален. В Javascript любой параметр опционален, но мы можем изменить это поведение, используя [**значения параметров по умолчанию из es2015**](http://exploringjs.com/es6/ch_parameter-handling.html#sec_parameter-default-values).

```javascript
const _err = function( message ){
  throw new Error( message );
}

const getSum = (a = _err('a не определен'), b = _err('b не определен')) => a + b

getSum( 10 ) // выкинет Error, b не определен
getSum( undefined, 10 ) // выкинет Error, a не определен
```

 `_err` — функция, которая сразу выкидывает ошибку. Если в функцию не был передан один из параметров, будет присвоено значение по умолчанию, в данном случае результат работы `_err`. Больше примеров с **параметрами по умолчанию** вы можете найти на [Mozilla's Developer Network](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/default_parameters)
