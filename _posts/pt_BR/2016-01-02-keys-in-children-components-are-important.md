---
layout: post

title: Keys in children components are important
tip-number: 02
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: Key é um atributo que você deve passar para todos os componentes criados dinamicamente a partir de um array. É um id único e constante que o React usa para identificar cada componente no DOM e saber quando é diferente ou o mesmo componente. Usar keys garante que o componente filho é preservado e não recriado prevenindo comportamentos não esperados.

categories:
    - pt_BR
---

[Key](https://facebook.github.io/react/docs/multiple-components.html#dynamic-children) é um atributo que você deve passar para todos os componentes criados dinamicamente a partir de um array. É um id único e constante que o React usa para identificar cada componente no DOM e saber quando é diferente ou o mesmo componente. Usar keys garante que o componente filho é preservado e não recriado prevenindo comportamentos não esperados.

> Key realmente não é sobre performance, é mais sobre identificar (que por sua vez leva a um melhor desempenho). Atribuição aleatória e mudança de valores não formam uma identidade [Paul O’Shannessy](https://github.com/facebook/react/issues/1342#issuecomment-39230939) (tradução literal)

- Use um valor único existente no objeto.
- Defina as keys no componente pai, não nos componentes filhos.

```javascript
//ruim
...
render() {
	<div key={{item.key}}>{{item.name}}</div>
}
...

//bom
<MyComponent key={{item.key}}/>
```
- [Usar índice de array é uma prática ruim.](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318#.76co046o9)
- `random()` não irá funcionar

```javascript
//ruim
<MyComponent key={{Math.random()}}/>
```

- Você pode criar seu próprio id único. Tenha certeza que o método é rápido e anexe ao seu objeto.
- Quando o número de filhos for grande ou conter muitos componentes, use keys para melhorar o desempenho.
- [Você deve fornecer o atributo key para todos os filhos de ReactCSSTransitionGroup.](http://docs.reactjs-china.com/react/docs/animation.html)