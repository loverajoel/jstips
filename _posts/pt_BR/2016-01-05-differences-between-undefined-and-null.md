---
layout: post

title: Diferenças entre `undefined` e `null`
tip-number: 05
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: Entendendo as diferenças entre `undefined` e `null`.

categories:
    - pt_BR
---

- `undefined` significa que a variável não foi declarada ou foi declarada mas ainda não foi atribuído um valor
- `null` é uma atribuição que significa "sem valor"
- Javascript seta variáveis com valor não atribuído como `undefined` por padrão
- Javascript nunca seta um valor como `null`. Ele é usado por programadores para indicar que uma `var` não tem valor.
- `undefined` não é válido em JSON enquanto `null` é
- `undefined` typeof é `undefined`
- `null` typeof é um `object`. [Por quê?](http://www.2ality.com/2013/10/typeof-null.html)
- Ambos são primitivos
- Ambos são [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)
  (`Boolean(undefined) // false`, `Boolean(null) // false`)
- Você pode saber se uma variável é [undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined,
  ```javascript
  typeof variable === "undefined"
```
- Você pode checar se uma variável é [null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null)

  ```javascript
  variable === null
```
- O **operador de igualdade** considera-os iguais, mas o **operador de igualdade estrita** não

  ```javascript
  null == undefined // true

  null === undefined // false
```