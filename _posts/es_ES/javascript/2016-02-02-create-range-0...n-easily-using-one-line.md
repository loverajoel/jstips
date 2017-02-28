---
layout: post

title: Crear rangos 0...(N-1) facilmente usando una linea
tip-number: 33
tip-username: SarjuHansaliya
tip-username-profile: https://github.com/SarjuHansaliya
tip-tldr: Podemos crear una función de rango que dará un rango entre 0...(N-1) utilizando una sola línea

redirect_from:
  - /es_es/create-range-0...n-easily-using-one-line/

categories:
    - es_ES
    - javascript
---

A continuación mostraremos como crear el rango 0...N-1).

```js
Array.apply(null, {length: N}).map(Number.call, Number);
```

Vamos a descomponer esta línea en partes. Sabemos como la funcion `call ()` trabaja en javascript. Así que en `call ()` el primer argumento será contexto y los segundos argumentos, será una lista de argumentos de la función en la que estamos llamando `call()`.

```js
function add(a, b){
    return (a+b);
}
add.call(null, 5, 6);
```
Esto devolverá una suma de 5 y 6.

`map()` del array en javascript toma dos argumentos, el primero `callback` y el segundo `thisArg(context)`. `callback` está tomando tres argumentos, `value`, `index` y todo el `array` sobre el que estamos iterando. Así es la sintaxis común:

```js
[1, 2, 3].map(function(value, index, arr){
    //Code
}, this);
```
Debajo de la línea crea array de longitud dada.

```js
Array.apply(null, {length: N})
```
Poner todas las partes juntas a continuación es la solución.

```js
Array.apply(null, {length: N}).map(Number.call, Number);
```

Si tiene un rango 1...N, que sera como este.

```js
Array.apply(null, {length: N}).map(function(value, index){
  return index+1;  
});
```
