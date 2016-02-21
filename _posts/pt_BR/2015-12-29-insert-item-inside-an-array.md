---
layout: post

title: Inserir item em um array
tip-number: 00
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: Inserir um item em um array existente é uma tarefa muito comum. Você pode adicionar elementos no final de um array usando push, no começo usando unshift ou no meio usando splice.


categories:
    - pt_BR
---

Inserir um item em um array existente é uma tarefa muito comum. Você pode adicionar elementos no final de um array usando push, no começo usando unshift ou no meio usando splice.

Estes são métodos conhecidos, mas não significa que não exista uma forma mais performática. Vamos lá:

Adicionar um elemento no final de um array é fácil com push(), mas há uma forma com melhor performance.

```javascript
var arr = [1,2,3,4,5];

arr.push(6);
arr[arr.length] = 6; // 43% mais rápido no Chrome 47.0.2526.106 no Mac OS X 10.11.1
```
Ambos os métodos modificam o array original. Não acredita? Veja o [jsperf](http://jsperf.com/push-item-inside-an-array)

Agora se estivermos tentando adicionar um item no começo do array:

```javascript
var arr = [1,2,3,4,5];

arr.unshift(0);
[0].concat(arr); // 98% mais rápido no Chrome 47.0.2526.106 no Mac OS X 10.11.1
```
Mais um detalhe: unshift edita o array original; concat retorna um novo array. [jsperf](http://jsperf.com/unshift-item-inside-an-array)

Adicionar itens na metade do array é simples com splice, e há uma maneira mais performática de fazer isto.

```javascript
var items = ['one', 'two', 'three', 'four'];
items.splice(items.length / 2, 0, 'hello');
```

Eu tentei executar estes testes em vários Browsers e SO e o resultado foi similar. Espero que estas dicas sejam úteis para você e o encoraje a realizar seus próprios testes de performance!