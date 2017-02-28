---
layout: post

title: Using JSON.Stringify
tip-number: 40
tip-username: vamshisuram
tip-username-profile: https://github.com/vamshisuram
tip-tldr: Create string from selected properties of JSON object.


redirect_from:
  - /en/using-json-stringify/

categories:
    - en
    - javascript
---

Let's say there is an object with properties "prop1", "prop2", "prop3".
We can pass __additional params__ to __JSON.stringify__ to selectively write properties of the object to string like:

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

The __"str"__ will contain only info on selected properties only.

Instead of array we can pass a function also.

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

```javascript
var str = JSON.stringify(obj, selectedProperties, '\t\t');

/* str output with double tabs in every line.
{
        "prop1": "value1",
        "prop2": "value2"
}
*/

```

