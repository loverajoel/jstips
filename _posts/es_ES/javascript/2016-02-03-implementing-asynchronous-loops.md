---
layout: post

title: Implementación de bucle asíncrono.
tip-number: 34
tip-username: madmantalking
tip-username-profile: https://github.com/madmantalking
tip-tldr: Puedes tener problemas al implementar bucles asíncronos.

redirect_from:
  - /es_es/implementing-asynchronous-loops/

categories:
    - es_ES
    - javascript
---

Vamos a probar a escribir una función asíncrona que imprime el valor del índice del bucle cada segundo.

```js
for (var i=0; i<5; i++) {
	setTimeout(function(){
		console.log(i); 
	}, 1000);
}  
```
La salida de los script antes mencionados resulta ser

```js
> 5
> 5
> 5
> 5
> 5
```
Así que esto definitivamente no funciona.

**Explicaci&oacute;n**

Cada timeout se refiere a la original `i`, no una copia. Por lo que el bucle de incrementos `i` hasta que llega a 5, entonces comienza a dar timeuot y utilizar el valor actual de `i` (que es 5).

Pues bien, este problema parece fácil. Una solución inmediata es almacenar en caché el índice de bucle en una variable temporal.

```js
for (var i=0; i<5; i++) {
	var temp = i;
 	setTimeout(function(){
		console.log(temp); 
	}, 1000);
}  
```
Pero de nuevo la salida de los script anteriores resulta ser

```js
> 4
> 4
> 4
> 4
> 4
```

Por lo tanto, eso no funciona bien, porque los bloques no crean un ámbito de aplicación y las variables de inicializadores se izan a la parte superior del scope. De hecho, el bloque anterior es el mismo que:

```js
var temp;
for (var i=0; i<5; i++) {
 	temp = i;
	setTimeout(function(){
		console.log(temp); 
  	}, 1000);
}  
```
**Soluci&oacute;n**

Hay algunas maneras diferentes para copiar `i`. La forma más común es la creación de un closure declarando una función que se le pasa `i` como un argumento. Aquí hacemos esto como una función de auto-llamada.

```js
for (var i=0; i<5; i++) {
	(function(num){
		setTimeout(function(){
			console.log(num); 
		}, 1000); 
	})(i);  
}  
```
En JavaScript, los argumentos se pasan por valor a una función. Así tipos primitivos como números, fechas, y las cadenas son básicamente copiados. Si los cambia dentro de la función, que no afecta el scope exterior. Los objetos son especiales: si la función cambia dentro de una propiedad, el cambio se refleja en todos los scopes.

Otro camino para esto sería con el uso de `let`.

```js
for (let i=0; i<5; i++) {
	var temp = i;
 	setTimeout(function(){
		console.log(temp); 
	}, 1000);
}  
```
