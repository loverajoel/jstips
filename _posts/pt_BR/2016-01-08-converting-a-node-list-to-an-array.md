---
layout: post

title: Convertendo uma lista de nós em array
tip-number: 08
tip-username: Tevko
tip-username-profile: https://twitter.com/tevko
tip-tldr: Aqui vai uma maneira rápida, segura e reutilizável para converter uma lista de nós em um array de elementos do DOM.

categories:
    - pt_BR
---

O método `querySelectorAll` retorna um objeto array-like chamado de lista de nós. Estas estruturas de dados são tratadas como "Array-like" porque elas se parecem com um array, mas não podem ser usadas com métodos de array como `map` e `forEach`. Aqui vai uma maneira rápida, segura e reutilizável para converter uma lista de nós em um array de elementos do DOM:

```javascript
const nodelist = document.querySelectorAll('div');
const nodelistToArray = Array.apply(null, nodelist);

// e então...

nodelistToArray.forEach(...);
nodelistToArray.map(...);
nodelistToArray.slice(...);

//etc...
```

O método `apply` é usado para passar um array de argumentos para uma função com um determinado valor de `this`. [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) diz que o `apply` recebe um objeto array-like, que é exatamente o que o `querySelectorAll` retorna. Uma vez que não precisamos especificar um valor para this no contexto da função, passamos `null` ou `0`. O resultado é uma array de elementos do DOM que contém todos os métodos de array disponíveis.

Se estiver usando ES2015 você pode usar o [operador spread `...`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)

```js
const nodelist = [...document.querySelectorAll('div')]; // returns a real array

//later on ..

nodelist.forEach(...);
nodelist.map(...);
nodelist.slice(...);

//etc...
```