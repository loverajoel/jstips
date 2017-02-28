---
layout: post

title: Template Strings
tip-number: 09
tip-username: JakeRawr
tip-username-profile: https://github.com/JakeRawr
tip-tldr: A partir de ES6, JS ahora tiene template strings.

redirect_from:
  - /es_es/template-strings/

categories:
    - es_ES
    - javascript
---

A partir de ES6, JS ahora tiene template strings

Ejemplo:
String normal

```javascript
var firstName = 'Jake';
var lastName = 'Rawr';
console.log('My name is ' + firstName + ' ' + lastName);
// My name is Jake Rawr
```
Template String

```javascript
var firstName = 'Jake';
var lastName = 'Rawr';
console.log(`My name is ${firstName} ${lastName}`);
// My name is Jake Rawr
```

Usted puede hacer strings multilínea sin `\n' y lógica simple (ie 2+3) en el interior `$ {}` en template strings.

Usted también es capaz de modificar la salida de template strings utilizando una función; se les llama [template strings etiquetados](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings#Tagged_template_strings), por ejemplo los usos de cadenas de la plantilla etiquetados.

Tambien puede leer mas sobre Template Strings [read](https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2).