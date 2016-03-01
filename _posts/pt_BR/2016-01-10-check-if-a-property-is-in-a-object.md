---
layout: post

title: Checar se uma propriedade está em um objeto
tip-number: 10
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: Estas são as formas de checar se uma propriedade está presente em um objeto.

categories:
    - pt_BR
---

Quando você tem de checar se uma propriedade está presente em um [object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects), você provavelmente faz algo assim:

```javascript
var meuObjeto = {
  nome: '@tips_js'
};

if (meuObjeto.nome) { ... }

```

Isto funciona, mas você deve saber que há duas formas nativas para isto, o [operador `in`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in) e o [`Object.hasOwnProperty`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty). Todo objeto descendente de `Object` pode ser checados das duas maneiras.

### Entenda a grande diferença

```javascript
var meuObjeto = {
  nome: '@tips_js'
};

meuObjeto.hasOwnProperty('nome'); // true
'nome' in meuObjeto; // true

meuObjeto.hasOwnProperty('valueOf'); // false, valueOf é herdado de protótipo
'valueOf' in meuObjeto; // true

```

A diferença está na profundidade em que cada uma checa a propriedade. Em outras palavras, `hasOwnProperty` somente retornará true se a propriedade estiver ligada diretamente à este objeto. Já para o operador `in` não importa se a propriedade foi criada no objeto ou herdada de um protótipo.

Outro exemplo:

```javascript
var minhaFuncao = function() {
  this.nome = '@tips_js';
};
minhaFuncao.prototype.idade = '10 days';

var usuario = new minhaFuncao();

usuario.hasOwnProperty('nome'); // true
usuario.hasOwnProperty('idade'); // false, porque idade vem de um protótipo
```

Confira os [exemplos em tempo real aqui](https://jsbin.com/tecoqa/edit?js,console)!

Também recomendo que leia [esta discussão](https://github.com/loverajoel/jstips/issues/62) sobre erros comuns quando se checa uma propriedade existente em um objeto.