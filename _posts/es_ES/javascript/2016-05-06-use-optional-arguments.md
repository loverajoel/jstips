---
layout: post

title: Cómo utilizar argumentos opcionales en funciones (con callback opcional)
tip-number: 54
tip-username: alphashuro
tip-username-profile: https://github.com/alphashuro
tip-tldr: Usted puede hacer argumentos de función y callback opcional

redirect_from:
  - /es_es/use-optional-arguments/

categories:
    - es_ES
    - javascript
---

Ejemplo de función donde los argumentos 2 y 3 son opcionales

```javascript
    function example( err, optionalA, optionalB, callback ) {
        // recuperar los argumentos como array
        var args = new Array(arguments.length);
        for(var i = 0; i < args.length; ++i) {
            args[i] = arguments[i];
        };
        
        // Primer argumento es el objeto de error
        // shift() elimina el primer elemento del
        // array y lo devuelve
        err = args.shift();

        // Si el último argumento es una función entonces es la funcion callback.
        // pop() elimina el último elemento del array
        // y lo devuelve
        if (typeof args[args.length-1] === 'function') { 
            callback = args.pop();
        }
        
        // Si args aún mantiene elementos, estos son
        // sus elementos opcionales que se podía
        // recuperar uno por uno como este:
        if (args.length > 0) optionalA = args.shift(); else optionalA = null;
        if (args.length > 0) optionalB = args.shift(); else optionalB = null;

        // continuar como de costumbre: comprobar si hay errores
        if (err) { 
            return callback && callback(err);
        }
        
        // para los propósitos de tutoría, ingrese los parámetros opcionales
        console.log('optionalA:', optionalA);
        console.log('optionalB:', optionalB);
        console.log('callback:', callback);

        /* haz tus cosas */

    }

    // ES6 con código más corto
    function example(...args) {
        // primer argumento es el objeto de error
        const err = args.shift();
        // si el último argumento es una función entonces es la funcion callback.
        const callback = (typeof args[args.length-1] === 'function') ? args.pop() : null;

        // args si todavía tiene elementos, estos son los elementos opcionales que se podía recuperar de uno en uno como este:
        const optionalA = (args.length > 0) ? args.shift() : null;
        const optionalB = (args.length > 0) ? args.shift() : null;
        // ... repetir para mas items

        if (err && callback) return callback(err);

        /* haz tus cosas */
    }

    // invocar la función de ejemplo con y sin argumentos opcionales
    
    example(null, 'AA');

    example(null, function (err) {   /* do something */    });

    example(null, 'AA', function (err) {});

    example(null, 'AAAA', 'BBBB', function (err) {});
```

### ¿Cómo se determina si optionalA o optionalB se destina?

El diseño de su función para requerir optionalA con el fin de aceptar optionalB