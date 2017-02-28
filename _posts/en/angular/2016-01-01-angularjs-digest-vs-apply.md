---
layout: post

title: AngularJs - `$digest` vs `$apply`
tip-number: 01
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: JavaScript modules and build steps are getting more numerous and complicated, but what about boilerplate in new frameworks?
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /en/angularjs-digest-vs-apply/

categories:
    - en
    - angular
---

One of the most appreciated features of AngularJs is the two-way data binding. In order to make this work AngularJs evaluates the changes between the model and the view through cycles(`$digest`). You need to understand this concept in order to understand how the framework works under the hood.

Angular evaluates each watcher whenever one event is fired. This is the known `$digest` cycle.
Sometimes you have to force it to run a new cycle manually and you must choose the correct option because this phase is one of the most influential in terms of performance.

### `$apply`
This core method lets you to start the digestion cycle explicitly. That means that all watchers are checked; the entire application starts the `$digest loop`. Internally, after executing an optional function parameter, it calls `$rootScope.$digest();`.

### `$digest`
In this case the `$digest` method starts the `$digest` cycle for the current scope and its children. You should notice that the parent's scopes will not be checked.
 and not be affected.

### Recommendations
- Use `$apply` or `$digest` only when browser DOM events have triggered outside of AngularJS.
- Pass a function expression to `$apply`, this has an error handling mechanism and allows integrating changes in the digest cycle.

```javascript
$scope.$apply(() => {
	$scope.tip = 'Javascript Tip';
});
```

- If you only need to update the current scope or its children, use `$digest`, and prevent a new digest cycle for the whole application. The performance benefit is self-evident.
- `$apply()` is a hard process for the machine and can lead to performance issues when there is a lot of binding.
- If you are using >AngularJS 1.2.X, use `$evalAsync`, which is a core method that will evaluate the expression during the current cycle or the next. This can improve your application's performance