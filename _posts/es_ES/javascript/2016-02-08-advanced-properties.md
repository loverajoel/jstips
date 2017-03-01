---
layout: post

title: Propiedades avanzadas de Javascript
tip-number: 39
tip-username: mallowigi
tip-username-profile: https://github.com/mallowigi
tip-tldr: Cómo añadir propiedades privadas, getters y setters de objetos.


redirect_from:
  - /es_es/advanced-properties/

categories:
    - es_ES
    - javascript
---

Es posible configurar las propiedades del objeto en Javascript, por ejemplo, para establecer las propiedades de ser pseudo-privada o de sólo lectura. Esta característica está disponible desde ECMAScript 5.1, por lo tanto, es soportado por todos los navegadores recientes.

Para ello, es necesario utilizar el método `defineProperty` del `Object` prototype de este modo:
```js
var a = {};
Object.defineProperty(a, 'readonly', {
  value: 15,
  writable: false
});

a.readonly = 20;
console.log(a.readonly); // 15
```

La sintaxis es la siguiente:
```js
Object.defineProperty(dest, propName, options)
```

o para múltiples definiciones:
```js
Object.defineProperties(dest, {
  propA: optionsA,
  propB: optionsB, //...
})
```

donde las opciones incluyen los siguientes atributos:
- *value*: si la propiedad no es una getter (ver abajo), value es un atributo obligatorio. `{a: 12}` === `Object.defineProperty(obj, 'a', {value: 12})`
- *writable*: establecer la propiedad como readonly. Tenga en cuenta que si la propiedad está en objetos anidados, sus propiedades siguen siendo editable.
- *enumerable*: establecer la propiedad como ocultos. Eso significa que bucles `for ... of` y `stringify` no incluirá el establecimiento con su resultado, pero la propiedad sigue ahí. Nota: Esto no significa que la propiedad es privada! Todavía puede ser accesible desde el exterior, sólo significa que no será impreso.
- *configurable*: establecer la propiedad como no modificable, por ejemplo, protegidos de la supresión o redefinición. Una vez más, si la propiedad es un objeto anidado, sus propiedades siguen siendo configurable.


Así que con el fin de crear una propiedad privada constante, se puede definir así:

```js
Object.defineProperty(obj, 'myPrivateProp', {value: val, enumerable: false, writable: false, configurable: false});
```

Además de la configuración de propiedades, `defineProperty` nos permite definir *propiedades dinámicas*, gracias al segundo parámetro que es una cadena. Por ejemplo, digamos que quiero crear propiedades de acuerdo con alguna configuración externa:

```js

var obj = {
  getTypeFromExternal(): true // illegal in ES5.1
}

Object.defineProperty(obj, getTypeFromExternal(), {value: true}); // ok

// For the example sake, ES6 introduced a new syntax:
var obj = {
  [getTypeFromExternal()]: true
}
```

¡Pero eso no es todo! propiedades avanzadas nos permite crear **getters** y **setters**, al igual que otros lenguajes de programación orientada a objetos! En ese caso, no se puede utilizar `writable`, `enumerable` y `configurable`, pero en su lugar:

```js
function Foobar () {
  var _foo; //  true private property

  Object.defineProperty(obj, 'foo', {
    get: function () { return _foo; }
    set: function (value) { _foo = value }
  });

}

var foobar = new Foobar();
foobar.foo; // 15
foobar.foo = 20; // _foo = 20
```

Aparte de la ventaja obvia de encapsulación y metodos de acceso avanzados, se dará cuenta de que no teníamos "call" de getter, en cambio, sólo la propiedad "get" sin paréntesis! ¡Esto es increíble! Por ejemplo, imaginemos que tenemos un objeto con propiedades anidadas largas, así:

```js
var obj = {a: {b: {c: [{d: 10}, {d: 20}] } } };
```

Ahora, en lugar de hacer `a.b.c[0].d` (donde una de las propiedades se pueden resolver como `undefined` y lanzar un error), que en su lugar puede crear un alias:

```js
Object.defineProperty(obj, 'firstD', {
  get: function () { return a && a.b && a.b.c && a.b.c[0] && a.b.c[0].d }
})

console.log(obj.firstD) // 10
```

### Nota
Si se define un getter sin un setter y todavía intenta establecer un valor, obtendrá un error! Esto es particularmente importante cuando se utilizan funciones auxiliares tales como `$.extend` o `_.merge`. ¡Ten cuidado!

### Links

- [defineProperty](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)
- [Defining properties in JavaScript](http://bdadam.com/blog/defining-properties-in-javascript.html)
