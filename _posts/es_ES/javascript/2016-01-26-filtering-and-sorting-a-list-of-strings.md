---
layout: post

title: Filtrar y ordenar una lista de Strings
tip-number: 26
tip-username: davegomez
tip-username-profile: https://github.com/davegomez
tip-tldr: Es posible que tenga una gran lista de nombres que necesitas filtrar con el fin de eliminar los duplicados y ordenarlos alfabéticamente.

redirect_from:
  - /filtering-and-sorting-a-list-of-strings/

categories:
    - es_ES
    - javascript
---

Es posible que tenga una gran lista de nombres que necesita filtrar con el fin de eliminar los duplicados y ordenarlos alfabéticamente.

En nuestro ejemplo vamos a utilizar una lista de **palabras clave reservadas de JavaScript** que podemos encontrar en las diferentes versiones del lenguage, pero como se puede observar, hay una gran cantidad de palabras clave duplicadas y no están organizados alfabéticamente. Así que esta es una lista perfecta de cadenas de probar este consejo JavaScript ([Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)).

```js
var keywords = ['do', 'if', 'in', 'for', 'new', 'try', 'var', 'case', 'else', 'enum', 'null', 'this', 'true', 'void', 'with', 'break', 'catch', 'class', 'const', 'false', 'super', 'throw', 'while', 'delete', 'export', 'import', 'return', 'switch', 'typeof', 'default', 'extends', 'finally', 'continue', 'debugger', 'function', 'do', 'if', 'in', 'for', 'int', 'new', 'try', 'var', 'byte', 'case', 'char', 'else', 'enum', 'goto', 'long', 'null', 'this', 'true', 'void', 'with', 'break', 'catch', 'class', 'const', 'false', 'final', 'float', 'short', 'super', 'throw', 'while', 'delete', 'double', 'export', 'import', 'native', 'public', 'return', 'static', 'switch', 'throws', 'typeof', 'boolean', 'default', 'extends', 'finally', 'package', 'private', 'abstract', 'continue', 'debugger', 'function', 'volatile', 'interface', 'protected', 'transient', 'implements', 'instanceof', 'synchronized', 'do', 'if', 'in', 'for', 'let', 'new', 'try', 'var', 'case', 'else', 'enum', 'eval', 'null', 'this', 'true', 'void', 'with', 'break', 'catch', 'class', 'const', 'false', 'super', 'throw', 'while', 'yield', 'delete', 'export', 'import', 'public', 'return', 'static', 'switch', 'typeof', 'default', 'extends', 'finally', 'package', 'private', 'continue', 'debugger', 'function', 'arguments', 'interface', 'protected', 'implements', 'instanceof', 'do', 'if', 'in', 'for', 'let', 'new', 'try', 'var', 'case', 'else', 'enum', 'eval', 'null', 'this', 'true', 'void', 'with', 'await', 'break', 'catch', 'class', 'const', 'false', 'super', 'throw', 'while', 'yield', 'delete', 'export', 'import', 'public', 'return', 'static', 'switch', 'typeof', 'default', 'extends', 'finally', 'package', 'private', 'continue', 'debugger', 'function', 'arguments', 'interface', 'protected', 'implements', 'instanceof'];
```

Dado que no queremos cambiar nuestra lista original, vamos a utilizar una función de orden superior llamado [`filter`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/filter), que devolverá un nuevo array  filtro basado en un predicado (* Función *) que se pasa a ella. El predicado comparará el índice de la palabra clave actual en la lista original con su `index` en la nueva lista y la pondra en un nuevo array sólo si los índices coinciden.

Por último vamos a ordenar la lista filtrada con ayuda de la funcion[`sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) que toma una función de comparación como el único argumento, devolviendo una lista ordenada alfabéticamente.

```js
var filteredAndSortedKeywords = keywords
  .filter(function (keyword, index) {
      return keywords.indexOf(keyword) === index;
    })
  .sort(function (a, b) {
      if (a < b) return -1;
      else if (a > b) return 1;
      return 0;
    });
```

**ES6** (ECMAScript 2015) usa [arrow functions](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions) se ve un poco mas simple:

```js
const filteredAndSortedKeywords = keywords
  .filter((keyword, index) => keywords.indexOf(keyword) === index)
  .sort((a, b) => {
      if (a < b) return -1;
      else if (a > b) return 1;
      return 0;
    });
```

Y esta es la lista final filtrada y ordenada de palabras clave JavaScript reservados:

```js
console.log(filteredAndSortedKeywords);

// ['abstract', 'arguments', 'await', 'boolean', 'break', 'byte', 'case', 'catch', 'char', 'class', 'const', 'continue', 'debugger', 'default', 'delete', 'do', 'double', 'else', 'enum', 'eval', 'export', 'extends', 'false', 'final', 'finally', 'float', 'for', 'function', 'goto', 'if', 'implements', 'import', 'in', 'instanceof', 'int', 'interface', 'let', 'long', 'native', 'new', 'null', 'package', 'private', 'protected', 'public', 'return', 'short', 'static', 'super', 'switch', 'synchronized', 'this', 'throw', 'throws', 'transient', 'true', 'try', 'typeof', 'var', 'void', 'volatile', 'while', 'with', 'yield']
```
