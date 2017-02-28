---
layout: post

title: Escuchar eventos DOM mas simple
tip-number: 51
tip-username: octopitus
tip-username-profile: https://github.com/octopitus
tip-tldr: Una forma elegante y fácil de manejar eventos DOM

redirect_from:
  - /es_es/DOM-event-listening-made-easy/

categories:
    - es_ES
    - javascript
---

Muchos de nosotros todavía están haciendo estas cosas:

- `element.addEventListener('type', obj.method.bind(obj))`
- `element.addEventListener('type', function (event) {})`
- `element.addEventListener('type', (event) => {})`

Los ejemplos anteriores, crean nuevos controladores de eventos anónimos que no pueden ser retirados cuando ya no sean necesarios. Esto puede causar problemas de rendimiento o errores lógicos inesperados, cuando los controladores que ya no es necesario puden ser accidentalmente activado mediante interacciones del usuario inesperados o [event bubbling](http://www.javascripter.net/faq/eventbubbling.htm)

Patrones de gestión de eventos más seguras son las siguientes:

Utilice una referencia:

```js
const handler = function () {
  console.log("Tada!")
}
element.addEventListener("click", handler)
// Later on
element.removeEventListener("click", handler)
```

Función llamada que remueve a sí mismo:

```js
element.addEventListener('click', function click(e) {
  if (someCondition) {
    return e.currentTarget.removeEventListener('click', click);
  }
});
```

Un mejor enfoque:

```js
function handleEvent (eventName, {onElement, withCallback, useCapture = false} = {}, thisArg) {
  const element = onElement || document.documentElement

  function handler (event) {
    if (typeof withCallback === 'function') {
      withCallback.call(thisArg, event)
    }
  }

  handler.destroy = function () {
    return element.removeEventListener(eventName, handler, useCapture)
  }

  element.addEventListener(eventName, handler, useCapture)
  return handler
}

// Anytime you need
const handleClick = handleEvent('click', {
  onElement: element,
  withCallback: (event) => {
    console.log('Tada!')
  }
})

// And anytime you want to remove it
handleClick.destroy()
```
