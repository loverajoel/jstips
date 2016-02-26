---
layout: post

title: Strings template
tip-number: 09
tip-username: JakeRawr
tip-username-profile: https://github.com/JakeRawr
tip-tldr: A partir do ES6, o JS tem strings template como uma alternativa às citações clássicas em strings.

categories:
    - pt_BR
---

A partir do ES6, o JS tem strings template como uma alternativa ao clássico de citações em strings.

Ex:
String normal

```javascript
var nome = 'Jake';
var sobrenome = 'Rawr';
console.log('Meu nome é ' + nome + ' ' + sobrenome);
// Meu nome é Jake Rawr
```
Template String

```javascript
var nome = 'Jake';
var sobrenome = 'Rawr';
console.log(`Meu nome é ${nome} ${sobrenome}`);
// Meu nome é Jake Rawr
```

Você pode utilizar strings multilinhas sem `\n` e lógica simples (ex 2+3) dentro de `${}` em strings templates.

Também é possível modificar a saída de strings template usando uma função; chama-se [tagged template strings]
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings#Tagged_template_strings), veja os exemplos de uso.

Você também pode querer [ler para entender](https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2) mais sobre strings template.