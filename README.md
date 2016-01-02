![header](https://raw.githubusercontent.com/loverajoel/jstips/master/resources/jstips-header-blog.gif)

# Introducing Javascript Tips
> New year, new project. **A JS tip per day!**

With great excitement, I introduce short and useful Javascript tips per day that will allow you to improve your code writing. With less than 2 minutes each day, you will be able to read about performance, frameworks, conventions, hacks, interview questions and all the items that future of this awesome language holds for us.

At midday, no matter if it is a weekend or a holiday, a tip will be posted and tweeted.

### Can you help us enrich it?
Please feel free to send us a PR with your own Javascript tip to be published here.
Any improvements or suggestions are more than welcome!
[Click to see the instructions](https://github.com/loverajoel/jstips/blob/master/CONTRIBUTING.md)

### Let’s keep in touch
To get updates, watch the repo and follow the [Twitter account](https://twitter.com/tips_js), only one tweet will be sent per day. It is a deal!
> Don't forget Star the repo, this will help to diffuse the project!

# Tips list

## #02 - ReactJs - Keys in children components are important

> 02/01/2016


The [key](https://facebook.github.io/react/docs/multiple-components.html#dynamic-children) is an attribute that you must pass to all components created dynamically from an array. It's unique and constant id that React use for identify each component in the DOM and know that it's a different component and not the same one. Using keys will ensure that the child component is preserved and not recreated and prevent that weird things happens.

> Key is not really about performance, it's more about identity (which in turn leads to better performance). randomly assigned and changing values are not identity [Paul O’Shannessy](https://github.com/facebook/react/issues/1342#issuecomment-39230939)

- Use an exisiting unique value of the object.
- Define the keys in the parent components, not in child components
	
	```javascript
	//bad
	...
	render() {
		<div key={{item.key}}>{{item.name}}</div>
	}
	...

	//good
	<MyComponent key={{item.key}}/>
	```
- [Use the array index is a bad practice.](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318#.76co046o9)
- `random()` will not work
	
	```javascript
	//bad
	<MyComponent key={{Math.random()}}/>
	```

- You can create your own unique id, be sure that the method be fast and attach it to your object.
- When the amount of child are big or involve expensive components, use keys has performance improvements.
- [You must provide the key attribute for all children of ReactCSSTransitionGroup.](http://docs.reactjs-china.com/react/docs/animation.html)

## #1 - AngularJs: `$digest` vs `$apply`

> 01/01/2016

One of the most appreciated features of AngularJs is the two way data binding. In order to make this work AngularJs evaluate the changes between the model and the view through of cycles(`$digest`). You need to understand this concept in order to understand how the framework works under the hood.

Angular evaluate each watcher whenever one event was fired, this is the known `$digest` cycle.
Sometimes you have to force to run a new cycle manually and you must choose the correct option because this phase is one of the most influential in terms of performance.

### `$apply`
This core method lets you to start the digestion cycle explicitly, that means that all watchers are checked, the entire application starts the `$digest loop`. Internally after execute an optional function parameter, call internally to `$rootScope.$digest();`.

### `$digest`
In this case the `$digest` method starts the `$digest` cycle for the current scope and its children. You should notice that the parents scopes will not be checked
 and not be affected.

### Recomendations
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


## #0 - Insert item inside an Array
> 12/29/2015

Insert an item into an existing array is a daily common task. You can add elements to the end of an array using push, to the beginning using unshift, or the middle using splice.

But those are known methods, doesn't mean there isn't a more performant way, here we go...

Add a element at the end of the array is easy with push(), but there is a way more performant.

```javascript
var arr = [1,2,3,4,5];

arr.push(6);
arr[arr.length] = 6; // 43% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
Both methods modify the original array. Don't believe me? Check the [jsperf](http://jsperf.com/push-item-inside-an-array)

Now we are trying to add a item to the beginning of the array

```javascript
var arr = [1,2,3,4,5];

arr.unshift(0);
[0].concat(arr); // 98% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
Here is a little bit detail, unshift edit the original array, concat return a new array. [jsperf](http://jsperf.com/unshift-item-inside-an-array)

Add items at the middle of an array is easy with splice and is the most performant way to do it.

```javascript
var items = ['one', 'two', 'three', 'four'];
items.splice(items.length / 2, 0, 'hello');
```
I tried to run these tests in various Browsers and OS and the results were similar. I hope this tips will be useful for you and encourage to perform your own tests!

### License
[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png)](http://creativecommons.org/publicdomain/zero/1.0/)
