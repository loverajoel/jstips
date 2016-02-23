---
layout: post

title: Use strict e relaxe
tip-number: 07
tip-username: nainslie
tip-username-profile: https://twitter.com/nat5an
tip-tldr: O Strict-mode permite que o desenvolvedor escreva "código seguro" mais facilmente.

categories:
    - pt_BR
---

O Strict-mode permite que o desenvolvedor escreva "código seguro" mais facilmente.

Por padrão, o JavaScript permite que o programador seja descuidado, por exemplo, quando não obriga que declaremos variáveis com "var" quando as criamos.  Enquanto isso pode parecer conveniente para um desenvolvedor iniciante, também pode ser a causa de muitos erros quando um nome de variável é escrito incorretamente ou acidentalmente referenciada fora do seu escopo.

Programadores gostam que o computador faça as coisas chatas, como checar erros em nosso código automaticamente. É isto que o "use strict" do JavaScript permite fazer, tornando nossos erros em erros de JavaScript.

Nós usamos esta diretiva adicionando isto no começo de um aquivo js:

```javascript
// Todo o código na sintaxe strict mode
"use strict";
var v = "Oi!  Eu sou um código em strict mode!";
```

ou dentro de uma função:

```javascript
function f()
{
  // Função na sintaxe strict mode
  'use strict';
  function aninhada() { return "E eu também!"; }
  return "Oi!  Eu sou uma função em strict mode!  " + aninhada();
}
function f2() { return "Eu não estou em strict mode."; }
```

Ao incluir esta diretiva em um arquivo ou função JavaScript, direcionamos o motor do JavaScript para executar em strict mode, que desativa um grupo de comportamentos geralmente indesejados em grandes projetos JavaScript. Entre outras coisas, strict mode muda os seguintes comportamentos:

* Variáveis só podem ser introduzidas precedidas de "var"
* Tentativa de escrever em propriedades somente de leitura gera erro
* Você deve chamar construtores com a palavra-chave "new"
* "this" não esta vinculado implicitamente ao objeto global
* Uso muito limitado de eval() permitido
* O protege de usar qualquer palavra reservada como nome de variáveis

Strict mode é ótimo para novos projetos, mas pode ser um desafio usá-lo em projetos antigos que ainda não o utiliza em muitos lugares. Também pode ser um problema se seu build concatena todos os arquivos js em um único arquivo, pois isso faz com que todos os arquivos sejam executados em strict mode.

Strict mode é uma declaração, mas uma expressão literal, ignorada por versões mais antigas do JavaScript. Ele é suportado em:

* Internet Explorer a partir da versão 10.
* Firefox a partir da versão 4.
* Chrome a partir da versão 13.
* Safari a partir da versão 5.1.
* Opera a partir da versão 12.

[Veja uma descrição mais completa do strict mode em MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode).