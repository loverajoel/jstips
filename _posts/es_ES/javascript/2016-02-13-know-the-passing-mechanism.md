---
layout: post

title: Conocer el mecanismo de paso
tip-number: 44
tip-username: bmkmanoj
tip-username-profile: https://github.com/bmkmanoj
tip-tldr: JavaScript solamente pasa por valor para ambos tipos primitiva y objeto (o referencia). En el caso de referencia el valor de referencia en sí se pasa por valor.

redirect_from:
  - /es_es/calculate-the-max-min-value-from-an-array/

categories:
    - es_ES
    - javascript
---

JavaScript es pass-by-value, técnicamente. No es ni pass-by-value, ni pass-by-reference, pasando por el verdadero sentido de estos términos. Para entender este mecanismo de paso, echar un vistazo a los siguientes dos fragmentos de código de ejemplo y las explicaciones.

### Ejemplo 1

```js

var me = {					// 1
	'partOf' : 'A Team'
}; 

function myTeam(me) {		// 2

	me = {					// 3
		'belongsTo' : 'A Group'
	}; 
} 	

myTeam(me);		
console.log(me);			// 4  : {'partOf' : 'A Team'}

```

En el ejemplo anterior, cuando `myTeam` se invoca, JavaScript es *pasar la referencia a* `me` *objeto como valor, ya que es un objeto* y la invocación de sí mismo crea dos referencias independientes para el mismo objeto, (aunque el nombre siendo el mismo aquí `me`, es engañosa y nos da la impresión de que es el único de referencia) y por lo tanto, la variable de referencia a sí mismos son independientes.

Cuando asignamos un nuevo objeto en la posición #`3`, estamos cambiando el valor de referencia en su totalidad dentro de la función `myTeam`, y no va a tener ningún impacto en el objeto original fuera de este scope de la función, desde donde fue aprobada y la referencia en el scope exterior se va a conservar el objeto original y por lo tanto la salida de `# 4'.


### Ejemplo 2

```js

var me = {					// 1
	'partOf' : 'A Team'
}; 

function myGroup(me) { 		// 2
	me.partOf = 'A Group';  // 3
} 

myGroup(me);
console.log(me);			// 4  : {'partOf' : 'A Group'}
	
```

En el caso de invocar `myGroup`, estamos pasando el objeto `me`. Pero a diferencia del escenario de ejemplo 1, nosotros no estamos asignando esta variable `me` a cualquier nuevo objeto, lo que significa efectivamente el valor de referencia de objeto dentro del scope de la funcion `myGroup` todavía es el valor de referencia del objeto original y cuando estamos modificando la propiedad dentro de este scope, que está modificando de manera efectiva la propiedad del objeto original. Por lo tanto, se obtiene la salida de #`7`.

Lo mismo ocurre si esto no prueba que Javascript es pass-by-reference? No, no lo es. Recuerde, *JavaScript pasa la referencia como valor, en el caso de objetos*. La confusión surge ya que se tiende a no entender completamente lo que pase por referencia. Esta es la razón exacta, algunos prefieren llamar a esto como *Call-by-sharing*.


*Publicacion del autor [js-by-examples](https://github.com/bmkmanoj/js-by-examples/blob/master/examples/js_pass_by_value_or_reference.md)*
