---
layout: post

title: Array media y promedio.
tip-number: 41
tip-username: soyuka
tip-username-profile: https://github.com/soyuka
tip-tldr: Calcula la media y el promedio de los valores de la matriz


redirect_from:
  - /es_es/array-average-and-median/

categories:
    - es_ES
    - javascript
---

Los siguientes ejemplos se basan en el siguiente array:

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
```

Para obtener el promedio, tenemos que resumir los números y luego dividir por el número de valores. Los pasos son los siguientes:
- obtener la longitud del array
- sumar los valores
- obtener el promedio (`suma/length`)

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
let sum = values.reduce((previous, current) => current += previous);
let avg = sum / values.length;
// avg = 28
```

O bien:

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
let count = values.length;
values = values.reduce((previous, current) => current += previous);
values /= count;
// avg = 28
```

Ahora, para obtener media los pasos son los siguientes:
- ordenar el array
- obtener la media aritmética de los valores medios

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
values.sort((a, b) => a - b);
let lowMiddle = Math.floor((values.length - 1) / 2);
let highMiddle = Math.ceil((values.length - 1) / 2);
let median = (values[lowMiddle] + values[highMiddle]) / 2;
// median = 13,5
```

Con un operador de bits:

```javascript
let values = [2, 56, 3, 41, 0, 4, 100, 23];
values.sort((a, b) => a - b);
let median = (values[(values.length - 1) >> 1] + values[values.length >> 1]) / 2
// median = 13,5
```
