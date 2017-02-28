---
layout: post

title: Convertir a numero de la forma mas rapida
tip-number: 23
tip-username: sonnyt
tip-username-profile: http://twitter.com/sonnyt
tip-tldr: La conversión de cadenas en números es muy común. La forma más fácil y rápida de lograr sería utilizar el operador +.

redirect_from:
  - /es_es/converting-to-number-fast-way/
  
categories:
    - es_ES
    - javascript
---

La conversión de cadenas en números es muy común. La forma más rápida ([jsPref](https://jsperf.com/number-vs-parseint-vs-plus/29)) y más fácil de lograr que sería utilizar el operador `+` (mas).

```javascript
var one = '1';

var numberOne = +one; // Number 1
```

You can also use the `-` (minus) operator which type-converts the value into number but also negates it.
También se puede utilizar el operador `-` (menos) qué convierte el valor en número, sino también la niega.

```javascript
var one = '1';

var negativeNumberOne = -one; // Number -1
```