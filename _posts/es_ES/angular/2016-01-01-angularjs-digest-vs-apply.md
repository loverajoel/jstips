---
layout: post

title: AngularJs - `$digest` vs `$apply`
tip-number: 01
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: Los pasos para crear modulos en Javascript son cada vez más numerosos y complicados, pero ¿qué hay de los boilerplate en los nuevos frameworks?
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /es_es/angularjs-digest-vs-apply/

categories:
    - es_ES
    - angular
---

Una de las características más apreciadas de AngularJS es el de dos vías de enlace de datos. Con el fin de hacer de este trabajo AngularJS evalúa los cambios entre el modelo y la vista a través de ciclos (`$digest`). Es necesario comprender este concepto con el fin de entender cómo funciona el framework bajo el capó.

Angular evalúa cada observador cuando se dispara un evento. Este es el conocido ciclo de `$digest`.
A veces hay que obligarlo a realizar un nuevo ciclo de forma manual y debe elegir la opción correcta porque esta fase es uno de los más influyentes en términos de rendimiento.

### `$apply`
Este método del core le permite iniciar el ciclo de digestión de forma explícita. Eso significa que todos los observadores son comprobados; toda la aplicación se inicia el `$digest loop`. Internamente, después de ejecutar un parámetro de la función opcional, se llama `$rootScope.$digest();`.

### `$digest`
En este caso, el método `$digest` inicia el ciclo `$digest` para el scope actual y sus descendientes. Usted debe notar que los padres scopes, no serán revisadas, y no se verá afectada.

### Recomendaciones
- Use `$apply` o `$digest` sólo cuando eventos del DOM han disparado fuera del AngularJS.
- Pasar una expresión de función a `$apply`, esto tiene un mecanismo de control de errores y permite la integración de los cambios en el ciclo de digestión.

```javascript
$scope.$apply(() => {
	$scope.tip = 'Javascript Tip';
});
```

- Si sólo necesita actualizar el scope actual o sus hijos, usar `$digest`, y evitar un nuevo ciclo de digest para toda la aplicación. La ventaja de rendimiento es evidente por sí mismo.
- `$apply()` es un proceso difícil para la máquina y puede conducir a problemas de rendimiento cuando hay una gran cantidad de unión.
- Si está utilizando >AngularJS 1.2.X, usar `$evalAsync`, que es un método básico que evaluará la expresión durante el ciclo actual o el siguiente. Esto puede mejorar el rendimiento de su aplicación.