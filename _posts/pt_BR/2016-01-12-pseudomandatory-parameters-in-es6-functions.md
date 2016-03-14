---
layout: post

title: Parâmetros pseudo obrigatórios em funções ES6
tip-number: 12
tip-username: Avraam Mavridis
tip-username-profile: https://github.com/AvraamMavridis
tip-tldr: Em muitas linguages de programação os parâmetros de uma função são obrigatórios por padrão e o desenvolvedor tem que definir explicitamente quando um parâmetro é opcional.

categories:
    - pt_BR
---

Em muitas linguages de programação os parâmetros de uma função são obrigatórios por padrão e o desenvolvedor tem que definir explicitamente quando um parâmetro é opcional. No Javascript, todo parâmentro é opcional, mas podemos mudar este comportamento sem mexer no corpo atual da função, tirando vantagem do [**valor padrão para parâmetros em ES6**](http://exploringjs.com/es6/ch_parameter-handling.html#sec_parameter-default-values).

```javascript
const _erro = function( mensagem ){
  throw new Error( mensagem );
}

const pegaSoma = (a = _erro('a não foi definido'), b = _erro('b não foi definido')) => a + b

pegaSoma( 10 ) // mostra Erro, b não foi definido
pegaSoma( undefined, 10 ) // mostra Erro, a não foi definido
 ```

`_err ` é uma função que lança um Error imediatamente. Se nenhum valor é passado para algum dos parâmetros, o valor padrão será usado,  `_err ` será chamado e um Error será lançado. Veja mais exemplos do **parâmetro padrão** em [Mozilla's Developer Network](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/default_parameters).