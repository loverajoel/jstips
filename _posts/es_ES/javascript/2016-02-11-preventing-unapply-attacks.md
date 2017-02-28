---
layout: post

title: La prevención de ataques de cancelar la aplicación
tip-number: 42
tip-username: emars 
tip-username-profile: https://twitter.com/marseltov
tip-tldr: Congelar la construcción en los prototypes.

redirect_from:
  - /es_es/preventing-unapply-attacks/

categories:
    - es_ES
    - javascript
---

Reemplazando el constructor de prototypes, código externo puede ocasionar que el código roto sea reescribiendo código para exponer y cambiar los argumentos ligados. Esto puede ser un problema serio que rompe las aplicaciones que funciona mediante el uso de métodos polyfill ES5.

```js
// example bind polyfill
function bind(fn) {
  var prev = Array.prototype.slice.call(arguments, 1);
  return function bound() {
    var curr = Array.prototype.slice.call(arguments, 0);
    var args = Array.prototype.concat.apply(prev, curr);
    return fn.apply(null, args);
  };
}


// unapply-attack
function unapplyAttack() {
  var concat = Array.prototype.concat;
  Array.prototype.concat = function replaceAll() {
    Array.prototype.concat = concat; // restore the correct version
    var curr = Array.prototype.slice.call(arguments, 0);
    var result = concat.apply([], curr);
    return result;
  };
}
```

La función anterior descarta el array `prev` desde el enlace que significa que cualquier `.concat`, la primera llamada concat siguiente utilizando el ataque cancelar la aplicación generará un error.

Usando [Object.freeze](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze), haciendo un objeto inmutable, se impide que cualquier sobreescritura de los objetos prototype.


```js
(function freezePrototypes() {
  if (typeof Object.freeze !== 'function') {
    throw new Error('Missing Object.freeze');
  }
  Object.freeze(Object.prototype);
  Object.freeze(Array.prototype);
  Object.freeze(Function.prototype);
}());
```

Puede leer mas [here](https://glebbahmutov.com/blog/unapply-attack/).
Aunque este concepto se llama 'ataque de cancelar la aplicación' debido a algún código de poder acceder a los closures que normalmente no estarían en su scope, es sobre todo un error considerar esto una característica de seguridad, debido a que no impedir que un atacante la ejecución de código con el que se extiende desde prototipos antes de la congelación ocurre, y también sigue teniendo el potencial para leer todos los scopes que utilizan diversas características del lenguaje. ECMA módulos darían aislamiento, que es mucho más fuerte que esta solución sin embargo sigue sin solucionar los problemas de los scripts de terceros.
