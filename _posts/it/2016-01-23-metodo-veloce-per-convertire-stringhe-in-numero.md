---
layout: post

titolo: Metodo veloce per convertire stringhe in numero
tip-numero: 23
tip-username: sonnyt
tip-username-profile: http://twitter.com/sonnyt
tip-tldr: Convertire delle stringhe in numero è estremamente comune. Il metodo più facile e veloce per fare ciò è usare l'operatore aritmetico `+` (più).

categoria:
    - it
---

Convertire delle stringhe in numero è estremamente comune. Il metodo più facile e veloce ([jsPref](https://jsperf.com/number-vs-parseint-vs-plus/29)) per fare ciò è usare l'operatore aritmetico `+` (più).

```javascript
var one = '1';

var numberOne = +one; // Number 1
```

Potete anche usare l'operatore aritmetico `-` (meno) che converte il tipo ma lo cambia pure di segno.

```javascript
var one = '1';

var negativeNumberOne = -one; // Number -1
```
