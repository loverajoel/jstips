---
layout: post

titolo: Inserire un elemento in un Array
tip-numero: 00
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: Inserire degli elementi dentro un array é un processo che si ripete giornalmente. Puoi aggiungere elementi alla fine di esso usando la funzione push, all'inizio usando unshift, o sennò nel mezzo usando splice.


categoria:
    - it
---

Inserire degli elementi dentro un array é un processo che si ripete giornalmente. Puoi aggiungere elementi alla fine di esso usando la funzione push, all'inizio usando unshift altrimenti nel mezzo usando splice.

Questi sono i metodi più conosciuti, ma questo non vuol dire che non esistano alternative più performanti. Vediamo:

Aggiungere un elemento alla fine di un array é facile usando push(), ma esiste un'alternativa più performante.

```javascript
var arr = [1,2,3,4,5];

arr.push(6);
arr[arr.length] = 6; // 43% più veloce in Chrome 47.0.2526.106 su Mac OS X 10.11.1
```
Entrambi i metodi modificano l'array originale. Non mi credete? Date un occhio a [jsperf](http://jsperf.com/push-item-inside-an-array)

Ora se provassimo ad aggiungere un elemento all'inizio di un array:

```javascript
var arr = [1,2,3,4,5];

arr.unshift(0);
[0].concat(arr); // 98% più veloce in Chrome 47.0.2526.106 su Mac OS X 10.11.1
```
Vediamo più in dettaglio: unshift modifica l'array originale; concat invece restituisce un nuovo array. [jsperf](http://jsperf.com/unshift-item-inside-an-array)

Aggiungere un elemento nel mezzo ad un array é facile con splice, e questo é il modo più performante per farlo.

```javascript
var items = ['one', 'two', 'three', 'four'];
items.splice(items.length / 2, 0, 'hello');
```

Ho eseguito queste prove in diversi Browsers e OS e i risultati sono stati simili. Spero che questi tips vi resteranno utili e vi incoraggeranno a sperimentarli!
