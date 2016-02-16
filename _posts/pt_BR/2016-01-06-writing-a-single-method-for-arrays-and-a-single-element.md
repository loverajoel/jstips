---
layout: post

title: Escrevendo um único método tanto para arrays quanto para elementos únicos
tip-number: 06
tip-username: mattfxyz
tip-username-profile: https://twitter.com/mattfxyz
tip-tldr: Ao invés de escrever um método para manipular array e outro para elementos únicos como parâmetro, escreva uma função que possa lidar com ambos. É parecido como algumas funções do jQuery funcionam (`css` modificará tudo que combinar com o seletor).

categories:
    - pt_BR
---

Ao invés de escrever um método para manipular array e outro para elementos únicos como parâmetro, escreva uma função que possa lidar com ambos. É parecido como algumas funções do jQuery funcionam (`css` modificará tudo que combinar com o seletor).

Você tem apenas que concatenar tudo em um array. `Array.concat` aceitará um array ou um elemento único.

```javascript
function imprimirMaiusculas(palavras) {
  var elements = [].concat(palavras);
  for (var i = 0; i < elements.length; i++) {
    console.log(elements[i].toUpperCase());
  }
}
```

`imprimirMaiusculas` agora está pronta para aceitar um único item ou um array de itens como parâmetro.

```javascript
imprimirMaiusculas("cacto");
// => CACTUS
imprimirMaiusculas(["cacto", "urso", "batata"]);
// => CACTUS
//  BEAR
//  POTATO
```
