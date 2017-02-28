---
layout: post

title: Utilice la desestructuración de los parámetros de función
tip-number: 43
tip-username: dislick 
tip-username-profile: https://github.com/dislick
tip-tldr: ¿Sabías que se puede utilizar una funcion de desestructuración de parametro parámetros?

redirect_from:
  - /es_es/use-destructuring-in-function-parameters/

categories:
    - es_ES
    - javascript
---

Estoy seguro que muchos de ustedes ya están familiarizados con el [ES6 Destructuring Assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment). ¿Sabías que también se puede utilizar en los parámetros de una función?

```javascript
var sayHello = function({ name, surname }) {
  console.log(`Hello ${name} ${surname}! How are you?`);
};

sayHello({
  name: 'John',
  surname: 'Smith'
});
```

Esto es grande para las funciones que aceptan un objeto de opciones.

> Tenga en cuenta que la asignación desestructurada aún no está disponible en Node.js y casi todos los navegadores. Sin embargo, puede usar `--harmony-destructuring` para Node.js si desea intentarlo por sí mismo ahora.