---
layout: post

title: AngularJs - `$digest` vs `$apply`
tip-number: 01
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: Módulos JavaScript y fases de compilación se están volviendo más numerosas y complicadas, pero ¿Que ocurre con los boilerplate en los nuevos frameworks?

categories:
    - es
---

Una de las más apreciadas características de AngularJs es bindeo de datos de doble sentido. Para poder hacer esta tarea, AngularJs evalua los cambios entre el modelo y la vista mediante ciclos(`$digest`). Tienes que entender este concepto para poder entender como el framework funciona por debajo.

Angular evalua cada observador donde quiera que un evento sea lanzado. Esto se conoce como ciclo `$digest`.
A veces teienes que forzar la ejecución de un nuevo ciclo manualmente y debes escoger la opción correcta por esta fase es una de las influyentes en lo que respecta al rendimiento.

### `$apply`
Este método troncal te permite iniciar el ciclo `$digest` explícitamente. Eso significa que todos los observadores son comprobados; toda la aplicación inicia el `$digest loop`. Internamente, después de ejecutar una función adicional como parámetro, invoca `$rootScope.$digest();`.

### `$digest`
En este caso el método `$digest` inicia el ciclo `$digest` para el contexto(scope) actual y sus hijos. Teniendo presente que los contextos(scopes) padre no serán comprobados y por lo tanto no se verán afectados.

### Recomendaciones
- Utiliza `$apply` o `$digest` sólo cuando el eventos del DOM se lancen fuera de AngularJs.
- Pasa una expresión de función a `$apply`, dispone de un mecanismo de manejo de excepciones y permite integrar cambios en el ciclo `digest`.

```javascript
$scope.$apply(() => {
	$scope.consejo = 'Consejo Javascript';
});
```

- Si sólo nececitas actualizar el contexto(scope) actual o sus hijos, utiliza `$digest` y evita que un nuevo ciclo de `$digest` se lance para toda la aplicación. El beneficio en rendimiento es más que evidente.
- `$apply()` es uin proceso intenso para la máquina y puede inducir problemas de rendimiento cuando hay demasiados bindeos.
- Si estas usando >AngularJS 1.2.X, usa `$evalAsync`, que te permite evaluar una expresión durante el ciclo actual o el siguiente. Puede suponer una mejora en el rendimiento de la aplicación.
