---
layout: post

title: Diferencias entre `undefined` y `null`
tip-number: 05
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: Comprendiendo las diferencias entre `undefined` y `null`.
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /es_es/differences-between-undefined-and-null/

categories:
    - es_ES
    - javascript
---

- `undefined` significa una variable no se ha declarado, o se ha declarado pero aún no se le ha asignado un valor
- `null` es un valor de asignación que significa "no value"
- Javascript establece variables no asignadas con un valor por defecto de `undefined`
- Javascript nunca se setea un valor de `null`. Es utilizado por los programadores para indicar que un `var` no tiene ningún valor.
- `undefined` no es válido en JSON, mientras que `null` si lo es
- `undefined` typeof es `undefined`
- `null` typeof es un `object`. [porque?](http://www.2ality.com/2013/10/typeof-null.html)
- Ambos son primitivos
- Ambos son [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)
  (`Boolean(undefined) // false`, `Boolean(null) // false`)
- Se puede saber si una variable es [undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)

  ```javascript
  typeof variable === "undefined"
```
- Puede comprobar si una variable es [null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null)

  ```javascript
  variable === null
```
- The **equality** operator considers them equal, but the **identity** doesn't
El operador **igualdad** considera iguales, pero la **identidad** no lo hace

  ```javascript
  null == undefined // true

  null === undefined // false
```