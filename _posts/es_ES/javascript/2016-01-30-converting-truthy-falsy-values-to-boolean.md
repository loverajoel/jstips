---
layout: post

title: Convertir valores truthy/falsy a boolean
tip-number: 30
tip-username: hakhag
tip-username-profile: https://github.com/hakhag
tip-tldr: Los operadores lógicos son una parte fundamental de JavaScript, aquí se puede ver una manera de obtener siempre un verdadero o falso, no importa lo que se le dio a él.


redirect_from:
  - /es_es/converting-truthy-falsy-values-to-boolean/
  
categories:
    - es_ES
    - javascript
---

Puede convertir un valor [truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) o [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) a verdadero booleano con el `!!` operador.

```js
!!"" // false
!!0 // false
!!null // false
!!undefined // false
!!NaN // false

!!"hello" // true
!!1 // true
!!{} // true
!![] // true
```

