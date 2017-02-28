---
layout: post

title: Utiles trucos para Console Logging
tip-number: 50
tip-username: zackhall
tip-username-profile: https://twitter.com/zthall
tip-tldr: Utiles técnicas utilizando breakpoints de coacción y condicionales.

redirect_from:
  - /es_es/helpful-console-log-hacks/

categories:
    - es_ES
    - javascript
---

## Usando breakpoints condicionales

Si usted quiere observar un valor por consola cada vez que una función se llama, puede utilizar puntos de breakpoints condicionales para hacer esto. Abran sus herramientas dev, encontrar la función que desea registrar datos en la consola y un breakpoints con la siguiente condición:

```js
console.log(data.value) && false
```

Un breakpoint condicional detiene el hilo página sólo si la condición se evalúa como verdadera. Así que mediante el uso de console.log('foo') && false está garantizado que dan como resultado false, ya que está poniendo el falso literal en la condición AND. Así que esto no va a hacer una pausa cuando es evaluado, pero va a registrar datos en la consola. Esto también se puede utilizar para contar cuántas veces se llama una función o una callback.


He aquí cómo se puede establecer un punto de interrupción condicional en [Edge](https://dev.windows.com/en-us/microsoft-edge/platform/documentation/f12-devtools-guide/debugger/#setting-and-managing-breakpoints "Managing Breakpoints in Edge"), [Chrome](https://developer.chrome.com/devtools/docs/javascript-debugging#breakpoints "Managing Breakpoints in Chrome"), [Firefox](https://developer.mozilla.org/en-US/docs/Tools/Debugger/How_to/Set_a_conditional_breakpoint "Managing Breakpoints in Firefox") y [Safari](https://developer.apple.com/library/mac/documentation/AppleApplications/Conceptual/Safari_Developer_Guide/Debugger/Debugger.html "Managing Breakpoints in Safari").

## Impresión de una variable a la consola

¿Alguna vez ha entrado una variable en la consola y no fueron capaces de simplemente ver el código de la función? La forma más rápida para ver el código de la función es la de coaccionar a una cadena mediante la concatenación con una cadena vacía.

```js
console.log(funcVariable + '');
```