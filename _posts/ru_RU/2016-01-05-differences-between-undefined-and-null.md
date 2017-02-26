---
layout: post

title: Различия между `undefined` и `null`
tip-number: 05
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: Понимание различий между `undefined` и `null`.
tip-writer-support: https://www.coinbase.com/loverajoel

categories:
    - ru_RU
---

- `undefined` значит, что переменная не была объявлена, или была объявлена, но без значения.
- `null` — присваемое значение, означающее "нет значения"
- По умолчанию JavaScript всем переменным без значения, установит значение `undefined`
- Javascript никогда не установит значение `null`. Оно используется программистами, чтобы показать, что переменная не имеет значения
- `undefined` не валиден в JSON, а `null` валиден
- тип `undefined` — `undefined`
- тип `null` — объект. [Почему?](http://www.2ality.com/2013/10/typeof-null.html)
- Оба примитивы
- Оба [ложны](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)
  (`Boolean(undefined) // false`, `Boolean(null) // false`)
- Вы можете узнать, если переменная [undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)

```javascript
typeof variable === "undefined"
```
- Вы можете проверить, если переменная [null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null)

```javascript
variable === null
```
- Оператор **сравнения** (==) считает их равными, но **строгое сравнение** (===) считает иначе.

```javascript
null == undefined // true

null === undefined // false
```
