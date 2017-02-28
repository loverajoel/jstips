---
layout: post

title: Acelerar las funciones recursivas con memoization
tip-number: 29
tip-username: hingsir
tip-username-profile: https://github.com/hingsir
tip-tldr: Fibonacci es muy familiar. Podemos escribir la siguiente función en 20 segundos, pero no eficiente. Se puede almacenar en caché los resultados previamente calculados para acelerarlo.


redirect_from:
  - /es_es/speed-up-recursive-functions-with-memoization/

categories:
    - es_ES
    - javascript
---

Fibonacci es muy familiar. podemos escribir la siguiente función en 20 segundos.

```js
var fibonacci = function(n){
    return n < 2 ? n : fibonacci(n-1) + fibonacci(n-2);
}
```
funciona, pero no es eficiente. Se pueden almacenar en caché los resultados previamente calculados para acelerarlo.

```js
var fibonacci = (function(){
    var cache = {
        0: 0,
        1: 1
    };
    return function self(n){
        return n in cache ? cache[n] : (cache[n] = self(n-1) + self(n-2));
    }
})()
```
También, podemos definir una función de orden superior que acepta una función como argumento y devuelve una versión memoized de la función.

```js
var memoize = function(func){
    var cache = {};
    return function(){
        var key = Array.prototype.slice.call(arguments).toString();
        return key in cache ? cache[key] : (cache[key] = func.apply(this,arguments));
    }
}
fibonacci = memoize(fibonacci);
```
Y hay una versión ES6 de la función memoize.

```js
var memoize = function(func){
    const cache = {};
    return (...args) => {
        const key = [...args].toString();
        return key in cache ? cache[key] : (cache[key] = func(...args));
    }
}
fibonacci = memoize(fibonacci);
```
podemos usar `memoize()` en muchas otras situciones
* GCD(Greatest Common Divisor)

```js
var gcd = memoize(function(a,b){
    var t;
    if (a < b) t=b, b=a, a=t;
    while(b != 0) t=b, b = a%b, a=t;
    return a;
})
gcd(27,183); //=> 3
```
* Calculo Factorial

```js
var factorial = memoize(function(n) {
    return (n <= 1) ? 1 : n * factorial(n-1);
})
factorial(5); //=> 120
```
