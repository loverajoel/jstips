---
layout: post

title: Keys en componentes secundarios son importantes
tip-number: 02
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: La key es un atributo que se debe pasar a todos los componentes creados dinámicamente a partir de un array. Es un identificador único y constante que React usa para identificar cada componente en el DOM y saber si se trata de un componente diferente o el mismo. Utilizando keys asegura que el componente secundario se conserve y no se cree nuevamente y evita que cosas extrañas sucedan.
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /es_es/keys-in-children-components-are-important/

categories:
    - es_ES
    - react
---

La [key](https://facebook.github.io/react/docs/multiple-components.html#dynamic-children) es un atributo que se debe pasar a todos los componentes creados dinámicamente a partir de un array. Es un identificador único y constante que React usa para identificar cada componente en el DOM y saber si se trata de un componente diferente o el mismo. Utilizando keys asegura que el componente secundario se conserve y no se cree nuevamente y evita que cosas extrañas sucedan.

> La key no es realmente sobre el rendimiento, es más acerca de la identidad (que a su vez conduce a un mejor rendimiento). Aleatoriamente asignados y los valores cambiantes no forman una identidad [Paul O’Shannessy](https://github.com/facebook/react/issues/1342#issuecomment-39230939)

- Utilice un valor único existente del objeto.
- Definir las keys de los componentes padre, no en los componentes secundarios

```javascript
//bad
...
render() {
	<div key={% raw %}{{item.key}}{% endraw %}>{% raw %}{{item.name}}{% endraw %}</div>
}
...

//good
<MyComponent key={% raw %}{{item.key}}{% endraw %}/>
```
- [Usar el indice de un array es una mala practica.](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318#.76co046o9)
- `random()` no funcionara.

```javascript
//bad
<MyComponent key={% raw %}{{Math.random()}}{% endraw %}/>
```

- Usted puede crear su propia única id. Asegúrese de que el método es rápido y adjuntarlo a su objeto.
- Cuando el número de children es grande o contiene componentes caros, utilice keys para mejorar el rendimiento.
- [Debe proporcionar el atributo clave para todos los children de ReactCSSTransitionGroup.](http://docs.reactjs-china.com/react/docs/animation.html)