---
layout: post

title: Funciones de flechas de direcciones.
tip-number: 14
tip-username: pklinger
tip-username-profile: https://github.com/pklinger/
tip-tldr: Introducido como una nueva característica en ES6, funciones de dirección pueden ser una herramienta muy útil para escribir más código en un menor número de líneas

redirect_from:
  - /es_es/fat-arrow-functions/

categories:
    - es_ES
    - javascript
---

Introducido como una nueva característica en ES6, funciones de dirección pueden ser una herramienta muy útil para escribir más código en un menor número de líneas. El nombre proviene de su sintaxis, `=>`, que es una "flecha", en comparación con una flecha delgada `->`. Algunos programas ya reconocen a este tipo de función de diferentes lenguajes como Haskell, como 'lambda expressions', o 'anonymous functions'. Se le llama en el anonimato, ya que estas funciones de dirección no tienen un nombre de función descriptiva.

### ¿Cuales son los beneficios?
* Sintaxis: menos LOC; no más escribir palabra clave `function` una y otra vez
* Semántica: captura de la palabra clave `this` del contexto que lo rodea

### Ejemplo de sintaxis sencilla
Have a look at these two code snippets, which do the exact same job, and you will quickly understand what fat arrow functions do:
Echar un vistazo a estos dos fragmentos de código, que hacen exactamente el mismo trabajo, y usted entenderá rápidamente qué hacen las funciones de dirección:

```javascript
// general syntax for fat arrow functions
param => expression

// may also be written with parentheses
// parentheses are required on multiple params
(param1 [, param2]) => expression


// using functions
var arr = [5,3,2,9,1];
var arrFunc = arr.map(function(x) {
  return x * x;
});
console.log(arr)

// using fat arrow
var arr = [5,3,2,9,1];
var arrFunc = arr.map((x) => x*x);
console.log(arr)
```

As you can see, the fat arrow function in this case can save you time typing out the parentheses as well as the function and return keywords. I would advise you to always write parentheses around the parameter inputs, as the parentheses will be needed for multiple input parameters, such as in `(x,y) => x+y`. It is just a way to cope with forgetting them in different use cases. But the code above would also work like this: `x => x*x`. So far, these are only syntactical improvements, which lead to fewer LOC and better readability.

Como se puede ver, la función de flecha en este caso le puede ahorrar tiempo a escribir los paréntesis, así como la palabras clave function y return. Yo aconsejaría escribir siempre paréntesis en torno a los parámetros de entrada, como serán necesarios los paréntesis para varios parámetros de entrada, como en `(x,y) => x+y`. Pero el código anterior también sería el siguiente: `x => x*x`. Hasta ahora, estos son sólo mejoras sintácticas, que conducen a menos LOC y una mejor legibilidad.

### Léxico de unión `this`

There is another good reason to use fat arrow functions. There is the issue with the context of `this`. With arrow functions, you don't need to worry about `.bind(this)` or setting `that = this` anymore, as fat arrow functions pick the context of `this` from the lexical surrounding. Have a look at the next [example] (https://jsfiddle.net/pklinger/rw94oc11/):
Hay otra buena razón para utilizar las funciones de dirección. No es el problema con el contexto de `this`. Con las funciones de dirección, usted no necesita preocuparse por `.bind(this)` o el ajuste `that = this`, ya que las funciones de dirección recogen el contexto de `this` del léxico de los alrededores. Echar un vistazo a la siguiente [example] (https://jsfiddle.net/pklinger/rw94oc11/):

```javascript

// globally defined this.i
this.i = 100;

var counterA = new CounterA();
var counterB = new CounterB();
var counterC = new CounterC();
var counterD = new CounterD();

// bad example
function CounterA() {
  // CounterA's `this` instance (!! gets ignored here)
  this.i = 0;
  setInterval(function () {
    // `this` refers to global object, not to CounterA's `this`
    // therefore starts counting with 100, not with 0 (local this.i)
    this.i++;
    document.getElementById("counterA").innerHTML = this.i;
  }, 500);
}

// manually binding that = this
function CounterB() {
  this.i = 0;
  var that = this;
  setInterval(function() {
    that.i++;
    document.getElementById("counterB").innerHTML = that.i;
  }, 500);
}

// using .bind(this)
function CounterC() {
  this.i = 0;
  setInterval(function() {
    this.i++;
    document.getElementById("counterC").innerHTML = this.i;
  }.bind(this), 500);
}

// fat arrow function
function CounterD() {
  this.i = 0;
  setInterval(() => {
    this.i++;
    document.getElementById("counterD").innerHTML = this.i;
  }, 500);
}
```

Para más información acerca de las funciones de dirección se puede encontrar en [MDN] (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions). To see different syntax options visit [this site] (http://jsrocks.org/2014/10/arrow-functions-and-their-scope/).