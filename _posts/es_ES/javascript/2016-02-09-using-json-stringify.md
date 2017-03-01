---
layout: post

title: Usando JSON.Stringify
tip-number: 40
tip-username: vamshisuram
tip-username-profile: https://github.com/vamshisuram
tip-tldr: Crear un string seleccionando propiedades de un objeto JSON.


redirect_from:
  - /es_es/using-json-stringify/

categories:
    - es_ES
    - javascript
---

Digamos que hay un objeto con propiedades"prop1", "prop2", "prop3".
Podemos pasarle __patrametro adicional__ a __JSON.stringify__ a escribir propiedades  selectiva del objeto a cadena como:

```javascript
var obj = {
    'prop1': 'value1',
    'prop2': 'value2',
    'prop3': 'value3'
};

var selectedProperties = ['prop1', 'prop2'];

var str = JSON.stringify(obj, selectedProperties);

// str
// {"prop1":"value1","prop2":"value2"}

```

__"str"__ sólo contendrá información sobre propiedades seleccionadas.

En lugar de un array podemos pasar una función también.

```javascript

function selectedProperties(key, val) {
    // the first val will be the entire object, key is empty string
    if (!key) {
        return val;
    }

    if (key === 'prop1' || key === 'prop2') {
        return val;
    }

    return;
}
```

The last optional param it takes is to modify the way it writes the object to string.
El último parámetro opcional se necesita si quiere modificar la forma en que se escribe el objeto de cadena.

```javascript
var str = JSON.stringify(obj, selectedProperties, '\t\t');

/* str output with double tabs in every line.
{
        "prop1": "value1",
        "prop2": "value2"
}
*/

```

