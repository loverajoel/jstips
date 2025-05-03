---
layout: post

titolo: Differenze tra `undefined` e `null`
tip-numero: 05
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: Capire le differenze tra `undefined` e `null`.

categoria:
    - it
---

- `undefined` significa che una variabile non è stata dichiarata, o è stata dichiarata ma non gli è stato ancora assegnato un valore
- `null` è un'assegnazione di valore che significa "nessun valore"
- Javascript assegna ad un variabile senza valore il valore `undefined`
- Javascript non assegna mai il valore `null`. È usato dai programmato per indicare che una `variabile` non ha un valore.
- `undefined` non è valido in JSON mentre `null` lo è
- Il tipo di `undefined` è `undefined`
- Il tipo di `null` è `object`. [Perchè?](http://www.2ality.com/2013/10/typeof-null.html)
- Entrambi sono tipi primitivi
- Entrambi sono [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)
  (`Boolean(undefined) // false`, `Boolean(null) // false`)
- Puoi sapere se una variabile è [undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)

  ```javascript
  typeof variable === "undefined"
```
- Puoi verificare se una variabile è [null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null)

  ```javascript
  variable === null
```
- L'operatore di **uguaglianza semplice** (==) li considera uguali, ma l'operatore di **uguaglianza stretta** (===) no

  ```javascript
  null == undefined // true

  null === undefined // false
```
