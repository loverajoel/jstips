---
layout: post

title: Obtener extensión de archivo
tip-number: 53
tip-username: richzw
tip-username-profile: https://github.com/richzw
tip-tldr: ¿Cómo conseguir la extensión del archivo de manera más eficiente?

redirect_from:
  - /es_es/get-file-extension/

categories:
    - es_ES
    - javascript
---

### Pregunta: ¿Cómo conseguir la extensión de archivo?

```javascript
var file1 = "50.xsl";
var file2 = "30.doc";
getFileExtension(file1); //returs xsl
getFileExtension(file2); //returs doc

function getFileExtension(filename) {
  /*TODO*/
}
```

### Solucion 1: Expresion regular

```js
function getFileExtension1(filename) {
  return (/[.]/.exec(filename)) ? /[^.]+$/.exec(filename)[0] : undefined;
}
```

### Solucion 2: Metodo `split`

```js
function getFileExtension2(filename) {
  return filename.split('.').pop();
}
```

Estas dos soluciones no podían manejar algunos casos extremos, aquí hay otra solución más robusta.

### Solucion 3: Metodos `slice`, `lastIndexOf`

```js
function getFileExtension3(filename) {
  return filename.slice((filename.lastIndexOf(".") - 1 >>> 0) + 2);
}

console.log(getFileExtension3(''));                            // ''
console.log(getFileExtension3('filename'));                    // ''
console.log(getFileExtension3('filename.txt'));                // 'txt'
console.log(getFileExtension3('.hiddenfile'));                 // ''
console.log(getFileExtension3('filename.with.many.dots.ext')); // 'ext'
```

_¿Como funciona?_

- [String.lastIndexOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/lastIndexOf) el método devuelve la última aparición del valor especificado (`'.'` en este caso). Devuelve `-1` si no se encuentra el valor.
- Los valores de retorno de `lastIndexOf` para el parámetro `'filename'` y `'.hiddenfile'` son `0` y `-1` respectivamente.[Zero-fill operador de desplazamiento a la derecha (>>>)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#%3E%3E%3E_%28Zero-fill_right_shift%29) transformará `-1` a `4294967295` y  `-2` a `4294967294`, aquí es un truco para asegurar el nombre del archivo sin cambios en esos casos extremos.
- [String.prototype.slice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice) extrae la extensión del índice que se calculó anteriormente. Si el índice es mayor que la longitud del nombre de archivo, el resultado es `""`.

### Comparación

| Solucion                                  | Parametros           | Resultados  |
| ----------------------------------------- |:-------------------:|:--------:|
| Solucion 1: Expresion regular            | ''<br>  'filename' <br> 'filename.txt' <br> '.hiddenfile' <br> 'filename.with.many.dots.ext' | undefined <br> undefined <br> 'txt' <br> 'hiddenfile' <br> 'ext' <br> |
| Solucion 2: Metodo `split`                | ''<br>  'filename' <br> 'filename.txt' <br> '.hiddenfile' <br> 'filename.with.many.dots.ext'            | '' <br> 'filename' <br> 'txt' <br> 'hiddenfile' <br> 'ext' <br> |
| Solucion 3: Metodos `slice`, `lastIndexOf` | ''<br>  'filename' <br> 'filename.txt' <br> '.hiddenfile' <br> 'filename.with.many.dots.ext'            | '' <br> '' <br> 'txt' <br> '' <br> 'ext' <br> |

### Demo de performance

[Here](https://jsbin.com/tipofu/edit?js,console) es la demostración de los códigos anteriores.

[Here](http://jsperf.com/extract-file-extension) es la prueba de rendimiento de esos 3 soluciones.

### Codigo

[How can I get file extensions with JavaScript](http://stackoverflow.com/questions/190852/how-can-i-get-file-extensions-with-javascript)
