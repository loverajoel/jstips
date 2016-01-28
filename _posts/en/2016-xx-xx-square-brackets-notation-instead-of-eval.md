---
layout: post

title: Square brackets notation instead of eval
tip-number: XX
tip-username: frikinside
tip-username-profile: https://github.com/frikinside
tip-tldr: Eval is possibly the most misused function in JavaScript, we use it to execute code in a string dynamically but most of the times we just don't need it. Square brackets notation as property accesors could be a proper alternative.

categories:
    - en
---

Eval is possibly the most misused function in JavaScript, we use it to execute code in a string dynamically but most of the times we just don't need it. Square brackets notation as property accesors could be a proper alternative.
Instead of using eval() we can use the square brackets notation for several and typical case of use. Let's see the most common cases and how we can avoid the evil.

### Access to forms and elements dynamically
Imagine a form with a list of inputs representing an entity in the backend. We use this a lot and we could put a sufix on the name of the element with the identifier.
Something like this:
```html
<input type="text" name="description_1" value="one description" />
<input type="text" name="description_2" value="two description" />
<input type="text" name="description_3" value="three description" />
```
So we made a c00l function that get an `id` as parameter and reset the value.
Just because we are really really evil we use `eval()` with malevolence.
```JavaScript
function coolFunction(id) {
  eval('document.forms[0].description_" + id + ".value = "description_reset"');
}
```

Of course, that worked! But we can use it without eval with square brackets notation:
```JavaScript
function coolFunction(id) {
  document.forms[0]["description_" + id].value = "description_reset";
}
```

With square brackets notation we can access the properties with string like a Dictionary, Hashtable or any other `key value pairs`.

### Invoke functions via string name
Let's say that we have several functions with differents operations and we have another function to act as a hub and call the needed function but the operation is a string parameter so what we do? We use eval? Let's see:
```JavaScript
function oneOperation(){ /* some code & logic */ }
function anotherOperation(){ /* some code & logic */ }
function JustAnotherGenericOperation(){ /* some code & logic */ }

function operationHub(operation){
  eval(operation)();
}
```
That's was easy! We have it working just fine! But... wait! Can we avoid use `eval()`? Yes it is, square brackets to the rescue!
```JavaScript
function oneOperation(){ /* some code & logic */ }
function anotherOperation(){ /* some code & logic */ }
function JustAnotherGenericOperation(){ /* some code & logic */ }

function operationHub(operation){
  window[operation]();
}
```
Just as simple and easy like the eval way.

There are a lot of use cases but all are the same:
- Property access: We can use square brackets notation really easy and in a similar way like the standart dot notation do!
- Function call: We can use square brackets notation agains. We just need to keep in mind that we need `window` for global scope.
