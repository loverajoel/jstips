---
layout: post

title: Operadores de Asignación
tip-number: 35
tip-username: hsleonis
tip-username-profile: https://github.com/hsleonis
tip-tldr: Asignación es muy común. A veces volvemos a escribir, perdemos tiempo los 'Programadores perezosos'. Por lo tanto, podemos utilizar algunos trucos para ayudarnos y hacer nuestro código más claro y más simple.

redirect_from:
  - /es_es/assignment-shorthands/

categories:
    - es_ES
    - javascript
---

Asignación es muy común. A veces volvemos a escribir, perdemos tiempo los 'Programadores perezosos'. Por lo tanto, podemos utilizar algunos trucos para ayudarnos y hacer nuestro código más claro y más simple.

Este es el uso similar de

````javascript
x += 23; // x = x + 23;
y -= 15; // y = y - 15;
z *= 10; // z = z * 10;
k /= 7; // k = k / 7;
p %= 3; // p = p % 3;
d **= 2; // d = d ** 2;
m >>= 2; // m = m >> 2;
n <<= 2; // n = n << 2;
n ++; // n = n + 1;
n --; n = n - 1;

````

### If-else (Usando operador ternario)

Esto es lo que se escribe de manera regular.

````javascript
var newValue;
if(value > 10) 
  newValue = 5;
else
  newValue = 2;
````

Podemos utilizar el operador ternario para que sea impresionante:

````javascript
var newValue = (value > 10) ? 5 : 2;
````

### Null, Undefined, Empty Checks

````javascript
if (variable1 !== null || variable1 !== undefined || variable1 !== '') {
     var variable2 = variable1;
}
````

Abreviación:

````javascript
var variable2 = variable1  || '';
````
P.D.: Si variable1 en un numero, luego controla primero si es 0

### Object Array Notation

En lugar de usar:

````javascript
var a = new Array();
a[0] = "myString1";
a[1] = "myString2";
````
Utilice:

````javascript
var a = ["myString1", "myString2"];
````

### Associative array

En lugar de usar:

````javascript
var skillSet = new Array();
skillSet['Document language'] = 'HTML5';
skillSet['Styling language'] = 'CSS3';
````

Utilice:

````javascript
var skillSet = {
    'Document language' : 'HTML5', 
    'Styling language' : 'CSS3'
};
````
