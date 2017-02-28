---
layout: post

title: Utilizar === en lugar de ==
tip-number: 24
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: El operador `==` (or `!=`) lleva a cabo una conversión automática de tipos si es necesario. El operador `===` (or `!==`) no va a realizar ninguna conversión. En él se compara el valor y el tipo, que podría considerarse más rápido ([jsPref](http://jsperf.com/strictcompare)) que `==`.

redirect_from:
  - /es_es/use_===_instead_of_==/

categories:
    - es_ES
    - javascript
---

El operador `==` (or `!=`) lleva a cabo una conversión automática de tipos si es necesario. El operador `===` (or `!==`) no va a realizar ninguna conversión. En él se compara el valor y el tipo, que podría considerarse más rápido ([jsPref](http://jsperf.com/strictcompare)) que `==`.

```js
[10] ==  10      // is true
[10] === 10      // is false

'10' ==  10      // is true
'10' === 10      // is false

 []  ==  0       // is true
 []  === 0       // is false

 ''  ==  false   // is true but true == "a" is false
 ''  === false   // is false 

```
