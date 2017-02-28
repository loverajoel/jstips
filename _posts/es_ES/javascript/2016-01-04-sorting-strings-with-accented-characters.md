---
layout: post

title: Ordenando cadenas con caracteres acentuados
tip-number: 04
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: Javascript tiene un método nativo **sort**  que permite ordenar matrices. Haciendo un simple `array.sort()` va a tratar a cada entrada del array como una cadena y va a tratar de ordenarla alfabéticamente. Pero cuando intenta ordenar un array de caracteres no ASCII obtendrá un resultado extraño.
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /es_es/sorting-strings-with-accented-characters/

categories:
    - es_ES
    - javascript
---

Javascript tiene un método nativo **[sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)** que permite ordenar arrays. Haciendo una simple `array.sort()` va a tratar a cada entrada de la matriz como una cadena y va a tratar de ordenarla alfabéticamente. También puede proporcionar la funcion [own custom sorting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort#Parameters).

```javascript
['Shanghai', 'New York', 'Mumbai', 'Buenos Aires'].sort();
// ["Buenos Aires", "Mumbai", "New York", "Shanghai"]
```

Pero cuando intenta para un array de caracteres no ASCII como esto `['E', 'a', 'U', 'c']`, se obtendrá un resultado extraño `[' c ',' e ',' A ',' U ']'. Eso sucede porque sort sólo funciona con el idioma Inglés.

Mire el siguiente ejemplo:

```javascript
// Spanish
['único','árbol', 'cosas', 'fútbol'].sort();
// ["cosas", "fútbol", "árbol", "único"] // bad order

// German
['Woche', 'wöchentlich', 'wäre', 'Wann'].sort();
// ["Wann", "Woche", "wäre", "wöchentlich"] // bad order
```

Afortunadamente, hay dos maneras de superar este comportamiento [localeCompare](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare) and [Intl.Collator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Collator).

> Ambos métodos tienen sus propios parámetros personalizados con el fin de configurarlo para que funcione adecuadamente.

### Usando `localeCompare()`

```javascript
['único','árbol', 'cosas', 'fútbol'].sort(function (a, b) {
  return a.localeCompare(b);
});
// ["árbol", "cosas", "fútbol", "único"]

['Woche', 'wöchentlich', 'wäre', 'Wann'].sort(function (a, b) {
  return a.localeCompare(b);
});
// ["Wann", "wäre", "Woche", "wöchentlich"]
```

### Usando `Intl.Collator()`

```javascript
['único','árbol', 'cosas', 'fútbol'].sort(Intl.Collator().compare);
// ["árbol", "cosas", "fútbol", "único"]

['Woche', 'wöchentlich', 'wäre', 'Wann'].sort(Intl.Collator().compare);
// ["Wann", "wäre", "Woche", "wöchentlich"]
```

- Para cada método se puede personalizar la ubicación.
- De acuerdo a [Firefox](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare#Performance) Intl.Collator es más rápida cuando se compara un gran número de cadenas.

Así que cuando se trabaja con arrays de cadenas en un idioma distinto del Inglés, recuerde utilizar este método para evitar la clasificación inesperado.