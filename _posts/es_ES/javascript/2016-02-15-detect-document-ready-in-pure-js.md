---
layout: post

title: Detectar cuando DOM esta listo en JS puro
tip-number: 46
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: La forma cross-browser para comprobar si el DOM se ha cargado en JavaScript puro.
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /es_es/basics-declarations/

categories:
    - es_ES
    - javascript
---

La forma cross-browser para comprobar si el documento se ha cargado en JavaScript puro utiliza [`readyState`](https://developer.mozilla.org/en-US/docs/Web/API/Document/readyState).

```js
if (document.readyState === 'complete') {
  // The page is fully loaded
}
```

Como detectar cuando el document esta listo...


```js
let stateCheck = setInterval(() => {
  if (document.readyState === 'complete') {
    clearInterval(stateCheck);
    // document ready
  }
}, 100);
```

o con [onreadystatechange](https://developer.mozilla.org/en-US/docs/Web/Events/readystatechange)...


```js
document.onreadystatechange = () => {
  if (document.readyState === 'complete') {
    // document ready
  }
};
```

Use `document.readyState === 'interactive'` para detectar cuando el DOM esta listo.
