---
layout: post

title: Invocar una funcion inmediatamente
tip-number: 25
tip-username: rishantagarwal 
tip-username-profile: https://github.com/rishantagarwal
tip-tldr: Denominado como "Iffy" >dudoso< (IIFE - expresión de la función invocada inmediatamente) es una expresión de la función anónima que se invoca inmediatamente y tiene algunos usos importantes en Javascript.


redirect_from:
  - /es_es/Using-immediately-invoked-function-expression/

categories:
    - es_ES
    - javascript
---

Denominado como "Iffy" >dudoso< (IIFE - expresión de la función invocada inmediatamente) es una expresión de la función anónima que se invoca inmediatamente y tiene algunos usos importantes en Javascript.

```javascript

(function() {
 // Do something​
 }
)()

```

Es una expresión de función anónima que se invoca de inmediato, y tiene algunos usos particularmente importantes en JavaScript.

El par de paréntesis que rodean la función anónima convierte la función anónima en una expresión de función o expresión variable. Así que en lugar de una simple función anónima en el scope global, o donde quiera que se definió, ahora tenemos una expresión de función sin nombre.

Similarly, we can even create a named, immediately invoked function expression:
Del mismo modo, podemos incluso crear una llamada expresión de función, inmediatamente invocado:

```javascript
(someNamedFunction = function(msg) {
	console.log(msg || "Nothing for today !!")
	}) (); // Output --> Nothing for today !!​
​
someNamedFunction("Javascript rocks !!"); // Output --> Javascript rocks !!
someNamedFunction(); // Output --> Nothing for today !!​
```

Mas detalles URL's - 
1. [Link 1](https://blog.mariusschulz.com/2016/01/13/disassembling-javascripts-iife-syntax) 
2. [Link 2](http://javascriptissexy.com/12-simple-yet-powerful-javascript-tips/) 

Performance:
[jsPerf](http://jsperf.com/iife-with-call)