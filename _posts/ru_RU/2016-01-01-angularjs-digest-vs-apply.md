---
layout: post

title: AngularJs - `$digest` vs `$apply`
tip-number: 01
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: JavaScript модули и этапы сборки становятся более многочисленными и сложными, а что насчет шаблонного кода в новых фрейморках?
tip-writer-support: https://www.coinbase.com/loverajoel

categories:
    - ru_RU
---

Одна из самых популярных особенностей AngularJS — двухстороннее связывание данных. Для того, чтобы это работало, AngularJS вычисляет изменения между моделью и view с помощью циклов (`$digest`). Вы должны понять этот концепт, чтобы понимать как фреймворк работает под капотом.

Angular исполняет каждого наблюдателя всякий раз, когда срабатывает событие. Это называется `$digest` цикл.
Иногда нужно вручную запустить новый цикл и вы должны выбрать правильный способ, потому что эта фаза одна из самых тяжелых в плане производительности.

### `$apply`

Этот метод ядра позволяет явно запустить цикл `$digest`. Это значит, что все наблюдатели проверены; все приложение начинает `$digest` цикл.
This core method lets you to start the digestion cycle explicitly. That means that all watchers are checked; the entire application starts the `$digest loop`. Internally, after executing an optional function parameter, it calls `$rootScope.$digest();`.

### `$digest`
В данном случае метод `$digest` запускает `$digest` цикл для текущей области видимости и всех вложенных. Области видимости уровнем выше не будут проверены и затронуты.

### Recommendations
- Используйте `$apply` или `$digest` только когда браузерные DOM события вызываются вне AngularJS.
- Передавайте функциональные выражения в `$apply`, у этого метода есть механизм ловли ошибок и он позволяет интегрировать изменения в `$digest` цикле.

```javascript
$scope.$apply(() => {
	$scope.tip = 'Javascript Tip';
});
```

- If you only need to update the current scope or its children, use `$digest`, and prevent a new digest cycle for the whole application. The performance benefit is self-evident.
- `$apply()` is a hard process for the machine and can lead to performance issues when there is a lot of binding.
- If you are using >AngularJS 1.2.X, use `$evalAsync`, which is a core method that will evaluate the expression during the current cycle or the next. This can improve your application's performance
