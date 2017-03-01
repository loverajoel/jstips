---
layout: post

title: Evaluación de Short circuit en JS.
tip-number: 27
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: Evaluación de Short-circuit dice, el segundo argumento se ejecuta o evalúa sólo si el primer argumento no es suficiente para determinar el valor de la expresión, cuando el primer argumento de AND (&&) la función se evalúa como falsa, el valor total debe ser falso; y cuando el primer argumento de la función OR (||) da como resultado true, el valor total debe ser verdad.

redirect_from:
  - /es_es/short-circiut-evaluation-in-js/

categories:
    - es_ES
    - javascript
---

[Evaluación Short-circuit](https://en.wikipedia.org/wiki/Short-circuit_evaluation) dice, el segundo argumento se ejecuta o evalúa sólo si el primer argumento no es suficiente para determinar el valor de la expresión: cuando el primer argumento de la función AND ('&&') se evalúa como falsa, el valor total debe ser falso; y cuando el primer argumento de la función OR ('||') da como resultado true, el valor total debe ser verdad.

Para el siguiente funcion `test` condición and `isTrue` y 'isFalse'.

```js
var test = true;
var isTrue = function(){
  console.log('Test is true.');
};
var isFalse = function(){
  console.log('Test is false.');
};

```
Usar logico AND - `&&`.

```js
// A normal if statement.
if(test){
  isTrue();    // Test is true
}

// Above can be done using '&&' as -

( test && isTrue() );  // Test is true
```
Usar logico OR - `||`.

```js
test = false;
if(!test){
  isFalse();    // Test is false.
}

( test || isFalse());  // Test is false.
```
La lógica OR también podría ser utilizado para establecer un valor predeterminado para el argumento de la función.

```js
function theSameOldFoo(name){ 
    name = name || 'Bar' ;
    console.log("My best friend's name is " + name);
}
theSameOldFoo();  // My best friend's name is Bar
theSameOldFoo('Bhaskar');  // My best friend's name is Bhaskar
```
La lógica AND podría ser utilizado para evitar excepciones utilizando las propiedades de undefined.
Ejemplo:-

```js
var dog = { 
  bark: function(){
     console.log('Woof Woof');
   }
};

// Calling dog.bark();
dog.bark(); // Woof Woof.

//But if dog is not defined, dog.bark() will raise an error "Cannot read property 'bark' of undefined."
// To prevent this, we can you &&.

dog&&dog.bark();   // This will only call dog.bark(), if dog is defined.

```
