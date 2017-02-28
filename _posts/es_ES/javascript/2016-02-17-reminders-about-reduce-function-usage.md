---
layout: post

title: Reducir el uso de la función incorporada
tip-number: 48
tip-username: darul75
tip-username-profile: https://twitter.com/darul75
tip-tldr: Algunos recordatorios sobre cómo usar la función de reducir

redirect_from:
  - /es_es/reminders-about-reduce-function-usage/

categories:
    - es_ES
    - javascript
---

Como está escrito en la documentación del método `reduce()` aplica una función contra un acumulador y cada valor del array (de izquierda a derecha) para reducirla a un solo valor.

### `reduce()`

[reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) la funcion acepta 2 parametros (M: mandatory, O: optional):

- (M) la callback **reducer function** para ser aplicada se ocupa de un par de anterior (el resultado de cálculo anterior) y el próximo elemento hasta el final de la lista.
- (O) un **initial value** para ser utilizado como el primer argumento de la primera llamada de la callback.

Así que vamos a ver un uso común y luego una más sofisticada.

### Uso común (acumulacion, concatenacion)

Estamos en el sitio web de Amazon (precios en $) y nuestro carrito esta completo, vamos a calcular el total.

```javascript
// my current amazon caddy purchases
var items = [{price: 10}, {price: 120}, {price: 1000}];

// our reducer function
var reducer = function add(sumSoFar, nextPrice) { return sumSoFar + nextPrice.price; };

// do the job
var total = items.reduce(reducer, 0);

console.log(total); // 1130
```

Reducir el parámetro de la función opcional era entero primitivo de tipo 0 en el primer caso, pero podría haber sido un objeto, un Array... en lugar de un tipo primitivo,
pero vamos a ver esto más adelante.

Ahora, recibí un cupón de descuento de $20.

```javascript
var total = items.reduce(reducer,-20);

console.log(total); // 1110
```

### Uso avanzado (combinacion)

Este segundo ejemplo de sintaxis se inspira en Redux [combineReducers](http://redux.js.org/docs/api/combineReducers.html) function [source](https://github.com/reactjs/redux/blob/master/src/combineReducers.js#L93).

La idea separar la función de reducer por detras en funciones individuales separadas y al final calcular una nueva *función reductor grande sola*.

Para ilustrar esto, vamos a crear un único objeto literal con algunas funciones reductoras capaz de calcular los precios totales en moneda distinta $, € ...

```javascript
var reducers = {
  totalInDollar: function(state, item) {
    state.dollars += item.price;
    return state;
  },
  totalInEuros : function(state, item) {
    state.euros += item.price * 0.897424392;
    return state;
  },
  totalInPounds : function(state, item) {
    state.pounds += item.price * 0.692688671;
    return state;
  },
  totalInYen : function(state, item) {
    state.yens += item.price * 113.852;
    return state;
  }
  // more...
};
```

Luego, creamos una nueva función navaja suiza

- Responsable de la aplicación de la funcion reduce en cada parial.
- Que devolverá una nueva callback de funcion reductor

```javascript
var combineTotalPriceReducers = function(reducers) {
  return function(state, item) {
    return Object.keys(reducers).reduce(
      function(nextState, key) {
        reducers[key](state, item);
        return state;
      },
      {}      
    );
  }
};
```

Ahora vamos a ver cómo usarla.

```javascript
var bigTotalPriceReducer = combineTotalPriceReducers(reducers);

var initialState = {dollars: 0, euros:0, yens: 0, pounds: 0};

var totals = items.reduce(bigTotalPriceReducer, initialState);

console.log(totals);

/*
Object {dollars: 1130, euros: 1015.11531904, yens: 127524.24, pounds: 785.81131152}
*/
```

Espero que este approach le puede dar otra idea de la utilización de la función reduce() para sus propias necesidades.

Su función reduce podía manejar un historial de cada cálculo por ejemplo, como se hace en Ramda Js [scan](http://ramdajs.com/docs/#scan) 

[JSFiddle to play with](https://jsfiddle.net/darul75/81tgt0cd/)
