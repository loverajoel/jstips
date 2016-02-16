---
layout: post

title: Ordenando strings com caracteres acentuados
tip-number: 04
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: Javascript tem o método nativo **sort** que permite ordenar arrays. Um simples `array.sort()` irá tratar cada item do array como uma string e ordená-los alfabeticamente. Mas quando tentamos ordenar um array com caracteres fora da tabela ASCII obtemos um resultado inesperado.

categories:
    - pt_BR
---

Javascript tem o método nativo **[sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)** que permite ordenar arrays. Um simples `array.sort()` irá tratar cada item do array como uma string e ordená-los alfabeticamente. Você também pode utilizar sua [própria função de ordenação](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort#Parameters).

```javascript
['Shanghai', 'New York', 'Mumbai', 'Buenos Aires'].sort();
// ["Buenos Aires", "Mumbai", "New York", "Shanghai"]
```

Mas quando tentamos ordenar um array com caracteres fora da tabela ASCII como este `['é', 'a', 'ú', 'c']`, obtemos um resultado inesperado `['c', 'e', 'á', 'ú']`. Isto acontece porque o sort funciona apenas com o idioma inglês.

Veja o próximo exemplo:

```javascript
// Spanish
['único','árbol', 'cosas', 'fútbol'].sort();
// ["cosas", "fútbol", "árbol", "único"] // ordem ruim

// German
['Woche', 'wöchentlich', 'wäre', 'Wann'].sort();
// ["Wann", "Woche", "wäre", "wöchentlich"] // ordem ruim
```

Felizmente, existem duas formas de evitar este comportamento: [localeCompare](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare) e [Intl.Collator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Collator) graças a ECMAScript Internationalization API.

> Ambos os métodos possuem seus próprios parâmetro personalizados, para que funcionem corretamente.

### Usando `localeCompare()`

```javascript
['único','árbol', 'cosas', 'fútbol'].sort(function (a, b) {
  return a.localeCompare(b);
});
// ["árbol", "cosas", "fútbol", "único"]

['Woche', 'wöchentlich', 'wäre', 'Wann'].sort(function (a, b) {
  return a.localeCompare(b);
});
// ["Wann", "wäre", "Woche", "wöchentlich"]
```

### Usando `Intl.Collator()`

```javascript
['único','árbol', 'cosas', 'fútbol'].sort(Intl.Collator().compare);
// ["árbol", "cosas", "fútbol", "único"]

['Woche', 'wöchentlich', 'wäre', 'Wann'].sort(Intl.Collator().compare);
// ["Wann", "wäre", "Woche", "wöchentlich"]
```

- Para cada método você pode customizar a localização.
- De acordo com o [Firefox](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare#Performance) Intl.Collator é mais rápido em comparações com uma grande quantidade de strings.

Portanto, quando estiver trabalhando com strings em outro idioma que não seja o inglês, lembre-se de usar este método para evitar uma ordenação incorreta.