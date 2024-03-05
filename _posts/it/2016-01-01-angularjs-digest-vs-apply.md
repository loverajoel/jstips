---
layout: post

titolo: AngularJs - `$digest` vs `$apply`
tip-numero: 01
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: I moduli e i passaggi per compilare in Javascript stanno diventando sempre più numerosi e complicati, ma che dire degli standard nei nuovi frameworks?

categoria:
    - it
---

Una delle funzionalità più apprezzate di AngularJs è il data binding bidirezionale (two-way data binding). Per fare ciò, AngularJs calcola i cambiamenti fra model e view attraverso cicli(`$digest`). È necessario conoscere questo concetto per capire come il framework funzioni al suo interno.

Angular calcola ogni watcher ogniqualvolta si verifica un evento. Questo è conosciuto come ciclo `$digest`.
Talvolta dovete forzare l'esecuzione manuale di un nuovo ciclo e scegliere l'opzione giusta perchè è da questo che dipendono le prestazioni del programma.

### `$apply`
Questo metodo vi permette di avviare il ciclo `$digest` esplicitamente. Questo significa che tutti i watchers sono verificati; l'intera applicazione fa partire il `$digest loop`. Internamente, dopo aver eseguito un parametro di funzione opzionale, viene richiamato il metodo `$rootScope.$digest();`.

### `$digest`
In questo caso il metodo `$digest` avvia il ciclo `$digest` per il corrente ambito e suoi figli. Noterete che gli ambiti del metodo padre non verrano verificati e influenzati.

### Raccomandazioni
- Usate `$apply` o `$digest` solamente quando gli eventi DOM del browser avvengono al di fuori di AngularJS.
- Passate un espressione a `$apply`, questo metodo supporta l'implementazione di un metodo di gestione degli errori e permette l'integrazione di cambiamenti nel ciclo digest.

```javascript
$scope.$apply(() => {
	$scope.tip = 'Javascript Tip';
});
```

- Se dovete solo aggiornare il corrente ambito o suoi figli, usate `$digest`, e prevenite un nuovo ciclo digest per l'intera applicazione. Migliori prestazioni saranno fin da subito evidenti.
- `$apply()` è un processo impegnativo per la macchina e può portare a problemi di prestazione quando vi sono molti legami.
- Se state usando >AngularJS 1.2.X, usate `$evalAsync`, è un metodo che eseguirà l'espressione durante il ciclo corrente o quello dopo. Questo può migliorare le prestazioni della vostra applicazione.
