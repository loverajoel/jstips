---
layout: post

title: Utilice strict y obtenga lazy
tip-number: 07
tip-username: nainslie
tip-username-profile: https://twitter.com/nat5an
tip-tldr: Modo estricto en JavaScript hace que sea más fácil para los desarrolladores para escribir "seguro".

redirect_from:
  - /es_es/use-strict-and-get-lazy/

categories:
    - es_ES
    - javascript
---

Modo estricto en JavaScript hace que sea más fácil para los desarrolladores para escribir "seguro".

De forma predeterminada, JavaScript permite al programador ser bastante descuidado, por ejemplo, al no requerir que declaremos nuestras variables con "var". Si bien esto puede parecer como una conveniencia para el desarrollador experimentado, que es también la fuente de muchos errores cuando un nombre de variable está mal escrito o accidentalmente se refirió a salir de su scope de aplicación.

Los programadores como para hacer que el ordenador haga las cosas aburridas para nosotros, y automáticamente comprobar nuestro trabajo por los errores. Eso es lo que el código JavaScript "use strict" directiva nos permite hacer, haciendo nuestros errores en errores de JavaScript.

Añadimos esta directiva ya sea que en la parte superior de un archivo JS:

```javascript
// Whole-script strict mode syntax
"use strict";
var v = "Hi!  I'm a strict mode script!";
```

o dentro de la funcion:

```javascript
function f()
{
  // Function-level strict mode syntax
  'use strict';
  function nested() { return "And so am I!"; }
  return "Hi!  I'm a strict mode function!  " + nested();
}
function f2() { return "I'm not strict."; }
```

Con la inclusión de esta directiva en un archivo o una función de JavaScript, vamos a dirigir el motor de JavaScript que se ejecutará en modo estricto que desactiva un grupo de comportamientos que son por lo general no deseable en proyectos de JavaScript más grandes. Entre otras cosas, el modo estricto cambia los siguientes comportamientos:

* Las variables sólo pueden ser introducidos cuando van precedidas con "var"
* El intento de escribir las propiedades de sólo lectura genera un error de ruido
* Tienes que llamar a los constructores con la palabra clave "new"
* "this" no está vinculado de manera implícita al objeto global
* Un uso permitido muy limitado de eval()
* Protege el uso de palabras reservadas o futuros palabras reservadas como nombres de variables

El modo estricto es ideal para nuevos proyectos, pero puede ser difícil de introducir en los proyectos más antiguos que aún no lo utilizan en la mayoría de lugares. También puede ser problemático si su cadena de acumulación concatena todos sus archivos js en un archivo grande, ya que esto puede causar todos los archivos que se ejecutan en modo estricto.

No es una declaración, sino una expresión literal, ignorada por las versiones anteriores de JavaScript.
El modo estricto se apoya en:

* Internet Explorer desde version 10.
* Firefox desde version 4.
* Chrome desde version 13.
* Safari desde version 5.1.
* Opera desde version 12.

[Ver MDN para una descripción más completa de modo estricto](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode).