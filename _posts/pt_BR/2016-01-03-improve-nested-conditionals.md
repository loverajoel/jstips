---
layout: post

title: Melhorar Condicionais Aninhados
tip-number: 03
tip-username: AlbertoFuente 
tip-username-profile: https://github.com/AlbertoFuente
tip-tldr: Como podemos melhorar e tornar mais eficiente a declaração de `if` aninhados em javascript?

categories:
    - pt_BR
---

Como podemos melhorar e tornar mais eficiente a declaração de `if` aninhados em javascript?

```javascript
if (cor) {
  if (cor === 'preto') {
    imprimirPreto();
  } else if (cor === 'vermelho') {
    imprimirVermelho();
  } else if (cor === 'azul') {
    imprimirAzul();
  } else if (cor === 'verde') {
    imprimirVerde();
  } else {
    imprimirAmarelo();
  }
}
```

Uma forma de melhorar declarações de `if` aninhados seria usar `switch`. Embora seja menos verboso e mais ordenado, o uso não é recomendado porque seu debug é muito difícil. [Aqui](https://toddmotto.com/deprecating-the-switch-statement-for-object-literals) o porquê.

```javascript
switch(cor) {
  case 'preto':
    imprimirPreto();
    break;
  case 'vermelho':
    imprimirVermelho();
    break;
  case 'azul':
    imprimirAzul();
    break;
  case 'verde':
    imprimirVerde();
    break;
  default:
    imprimirAmarelo();
}
```

Mas e se tivermos uma condicional com várias avaliações em cada declaração? Nesse caso, se quisermos algo menos verboso e mais ordenado, podemos usar o condicional `switch`.
Se passarmos `true` como um parâmetro para o `switch`, ele nos permitirá usar uma condicional em cada caso.

```javascript
switch(true) {
  case (typeof cor === 'string' && cor === 'preto'):
    imprimirPreto();
    break;
  case (typeof cor === 'string' && cor === 'vermelho'):
    imprimirVermelho();
    break;
  case (typeof cor === 'string' && cor === 'azul'):
    imprimirAzul();
    break;
  case (typeof cor === 'string' && cor === 'verde'):
    imprimirVerde();
    break;
  case (typeof cor === 'string' && cor === 'amarelo'):
    imprimirAmarelo();
    break;
}
```

Mas devemos sempre evitar muitas verificações em cada condição e evitar `switch` sempre que possível. Também devemos levar em conta que a forma mais eficiente de fazer isto é usando um `object`.

```javascript
var corObj = {
  'preto': imprimirPreto,
  'vermelho': imprimirVermelho,
  'azul': imprimirAzul,
  'verde': imprimirVerde,
  'amarelo': imprimirAmarelo
};

if (cor in corObj) {
  corObj[cor]();
}
```

[Aqui](http://www.nicoespeon.com/en/2015/01/oop-revisited-switch-in-js/) você pode encontrar mais informações sobre isto.
