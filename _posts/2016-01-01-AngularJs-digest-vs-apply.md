---
layout: default
title: "AngularJs: \'$digest\' vs \'$apply\'"
author: "@loverajoel"
author-link: https://twitter.com/loverajoel
---

One of the most appreciated features of AngularJs is the two way data binding. In order to make this work AngularJs evaluates the changes between the model and the view through cycles(`$digest`). You need to understand this concept in order to understand how the framework works under the hood.

Angular evaluates each watcher whenever one event is fired, this is the known `$digest` cycle.
Sometimes you have to force to run a new cycle manually and you must choose the correct option because this phase is one of the most influential in terms of performance.

### `$apply`
This core method lets you to start the digestion cycle explicitly, that means that all watchers are checked, the entire application starts the `$digest loop`. Internally after execute an optional function parameter, call internally to `$rootScope.$digest();`.

### `$digest`
In this case the `$digest` method starts the `$digest` cycle for the current scope and its children. You should notice that the parents scopes will not be checked
 and not be affected.

### Recommendations
- Use `$apply` or `$digest` only when browser DOM events have triggered outside of AngularJS.
- Pass a function expression to `$apply`, this have a error handling mechanism and allow integrate changes in the digest cycle

	```javascript
	$scope.$apply(() => {
		$scope.tip = 'Javascript Tip';
	});
	```

- If only needs update the current scope or its children use `$digest`, and prevent a new digest cycle for the whole application. The performance benefit it's self evident
- `$apply()` is hard process for the machine and can lead to performance issues when having a lot of binding.
- If you are using >AngularJS 1.2.X, use `$evalAsync` is a core method that will evaluate the expression during the current cycle or the next. This can improve your application's performance.
