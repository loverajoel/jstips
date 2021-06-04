---
layout: post

titolo: Concatenazione stringhe sicura
tip-numero: 19
tip-username: gogainda
tip-username-profile: https://twitter.com/gogainda
tip-tldr: Supponete di avere un paio di variabili di tipo non conosciuto e di volerle unire in una stringa. Per essere sicuri che delle operazioni aritmetiche non vengano eseguite, usate concat

categoria:
    - it
---

Supponete di avere un paio di variabili di tipo non conosciuto e di volerle unire in una stringa. Per essere sicuri che delle operazioni aritmetiche non vengano eseguite, usate `concat`:

```javascript
var one = 1;
var two = 2;
var three = '3';

var result = ''.concat(one, two, three); //"123"
```

In questo modo la concatenazione avviene nel modo corretto. Al contrario, la concatenazione usando dei segni aritmetici e senza usare `concat` può portare a risultati inaspettati:

```javascript
var one = 1;
var two = 2;
var three = '3';

var result = one + two + three; //"33" instead of "123"
```

Parlando di prestazioni, comparando il metodo `join` con concat, la velocità di `concat` è pressochè uguale. [Approfondimento](http://www.sitepoint.com/javascript-fast-string-concatenation/).

Potete approfondire il metodo `concat` su MDN [page](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/concat).
