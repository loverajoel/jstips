![header](https://raw.githubusercontent.com/loverajoel/jstips/master/resources/jstips-header-blog.gif)

# Introducing Javascript Tips
> New year, new project. **A JS tip per day!**

With great excitement, I introduce these short and useful daily Javascript tips that will allow you to improve your code writing. With less than 2 minutes each day, you will be able to read about performance, frameworks, conventions, hacks, interview questions and all the items that the future of this awesome language holds for us.

At midday, no matter if it is a weekend or a holiday, a tip will be posted and tweeted.

### Can you help us enrich it?
Please feel free to send us a PR with your own Javascript tip to be published here.
Any improvements or suggestions are more than welcome!
[Click to see the instructions](https://github.com/loverajoel/jstips/blob/master/CONTRIBUTING.md)

### Let’s keep in touch
To get updates, watch the repo and follow the [Twitter account](https://twitter.com/tips_js), only one tweet will be sent per day. It is a deal!
> Don't forget to Star the repo, as this will help to promote the project!

# Tips list

## #10 - Check if a property is in a Object

> 2016-01-10 by [@loverajoel](https://www.twitter.com/loverajoel)

When you have to check if a property is present of an [object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects), you probably are doing something like this:

```javascript
var myObject = {
  name: '@tips_js'
};
if (typeof myObject['name'] !== 'undefined') { ... }

if (myObject['name']) { ... }

```

Thats ok, but you have to know that there are two native methods for this kind of thing, [`Object.in`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in) and [`Object.hasOwnProperty`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty), every object descended from Object, has available both methods.

### See the big Difference
 
```javascript
var myObject = {
  name: '@tips_js'
};

myObject.hasOwnProperty('name'); // true
'name' in myObject; // true

myObject.hasOwnProperty('valueOf'); // false, valueOf is inherited from the prototype chain
'valueOf' in myObject; // true

```

Both differs in the depth how check the properties, in other words `hasOwnProperty` will only return true if key is available on that object directly, however `in` operator doesn't discriminate between properties created on an object and properties inherited from the prototype chain.

Here another example

```javascript
var myFunc = function() {
  this.name = '@tips_js';
};
myFunc.prototype.age = '10 days';

var user = new myFunc();

user.hasOwnProperty('name'); // true
user.hasOwnProperty('age'); // false, because age is from the prototype chain
```

Check here the [live examples](https://jsbin.com/tecoqa/edit?js,console)!

## #09 - Template Strings

> 2016-01-09 by [@JakeRawr](https://github.com/JakeRawr)

As of ES6, JS now has template strings as an alternative to the classic end quotes strings.

Ex: 
Normal string
```javascript
var firstName = 'Jake';
var lastName = 'Rawr';
console.log('My name is ' + firstName + ' ' + lastName);
// My name is Jake Rawr
```
Template String
```javascript
var firstName = 'Jake';
var lastName = 'Rawr';
console.log(`My name is ${firstName} ${lastName}`);
// My name is Jake Rawr
```

You can do Multi-line strings without `\n` and simple logic (ie 2+3) inside `${}` in Template String.

You are also able to to modify the output of template strings using a function; they are called [Tagged template strings]
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings) for example usages of tagged template strings.

You may also want to [read](https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2) to understand template strings more

## #08 - Converting a Node List to an Array

> 2016-01-08 by [@Tevko](https://twitter.com/tevko)

The `querySelectorAll` method returns an array-like object called a node list. These data structures are referred to as "Array-like", because they appear as an array, but can not be used with array methods like `map` and `foreach`. Here's a quick, safe, and reusable way to convert a node list into an Array of DOM elements:

```javascript
const nodelist = document.querySelectorAll('div');
const nodelistToArray = Array.apply(null, nodelist);

//later on ..

nodelistToArray.forEach(...);
nodelistToArray.map(...);
nodelistToArray.slice(...);

//etc...
```

The `apply` method is used to pass an array of arguments to a function with a given `this` value. [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) states that `apply` will take an array like object, which is exactly what `querySelectorAll` returns. Since we don't need to specify a value for `this` in the context of the function, we pass in `null` or `0`. The result is an actual array of DOM elements which contains all of the available array methods.

## #07 - "use strict" and get lazy

> 2016-01-07 by [@nainslie](https://twitter.com/nat5an)

Strict-mode JavaScript makes it easier for the developer to write "secure" JavaScript.

By default, JavaScript allows the programmer to be pretty careless, for example, by not requiring us to declare our variables with "var" when we first introduce them.  While this may seem like a convenience to the unseasoned developer, it's also the source of many errors when a variable name is misspelled or accidentally referred to out of its scope.

Programmers like to make the computer do the boring stuff for us, and automatically check our work for mistakes. That's what the JavaScript "use strict" directive allows us to do, by turning our mistakes into JavaScript errors.

We add this directive either by adding it at the top of a js file:

```javascript
// Whole-script strict mode syntax
"use strict";
var v = "Hi!  I'm a strict mode script!";
```

or inside a function:

```javascript
function f()
{
  // Function-level strict mode syntax
  'use strict';
  function nested() { return "And so am I!"; }
  return "Hi!  I'm a strict mode function!  " + nested();
}
function f2() { return "I'm not strict."; }
```

By including this directive in a JavaScript file or function, we will direct the JavaScript engine to execute in strict mode which disables a bunch of behaviors that are usually undesirable in larger JavaScript projects.  Among other things, strict mode changes the following behaviors:
* Variables can only be introduced when they are preceded with "var"
* Attempting to write to readonly properties generates a noisy error
* You have to call constructors with the "new" keyword
* "this" is not implicitly bound to the global object
* Very limited use of eval() allowed
* Protects you from using reserved words or future reserved words as variable names

Strict mode is great for new projects, but can be challenging to introduce into older projects that don't already use it in most places.  It also can be problematic if your build chain concatenates all your js files into one big file, as this may cause all files to execute in strict mode.

It is not a statement, but a literal expression, ignored by earlier versions of JavaScript.
Strict mode is supported in:
* Internet Explorer from version 10.
* Firefox from version 4.
* Chrome from version 13.
* Safari from version 5.1.
* Opera from version 12.

[See MDN for a fuller description of strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode).

## #06 - Writing a single method for arrays or single elements

> 2016-01-06 by [@mattfxyz](https://twitter.com/mattfxyz)

Rather than writing separate methods to handle an array and a single element parameter, write your functions so they can handle both. This is similar to how some of jQuery's functions work (`css` will modify everything matched by the selector).

You just have to concat everything into an array first. `Array.concat` will accept an array or a single element.

```javascript
function printUpperCase(words) {
  var elements = [].concat(words);
  for (var i = 0; i < elements.length; i++) {
    console.log(elements[i].toUpperCase());
  }
}
```

`printUpperCase` is now ready to accept a single node or an array of nodes as its parameter.

```javascript
printUpperCase("cactus");
// => CACTUS
printUpperCase(["cactus", "bear", "potato"]);
// => CACTUS
//  BEAR
//  POTATO
```

## #05 - Differences between `undefined` and `null`

> 2016-01-05 by [@loverajoel](https://twitter.com/loverajoel)

- `undefined` means a variable has not been declared, or has been declared but has not yet been assigned a value
- `null` is an assignment value that means "no value"
- Javascript sets unassigned variables with a default value of `undefined`
- Javascript never sets a value to `null`. It is used by programmers to indicate that a `var` has no value.
- `undefined` is not valid in JSON while `null` is
- `undefined` typeof is `undefined`
- `null` typeof is an `object`
- Both are primitives
- Both are [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)
  (`Boolean(undefined) // false`, `Boolean(null) // false`)
- You can know if a variable is [undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)

  ```javascript
  typeof variable === "undefined"
```
- You can check if a variable is [null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null)

  ```javascript
  variable === null
```
- The **equality** operator considers them equal, but the **identity** doesn't

  ```javascript
  null == undefined // true

  null === undefined // false
```

## #04 - Sorting strings with accented characters

> 2016-01-04 by [@loverajoel](https://twitter.com/loverajoel)

Javascript has a native method **[sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)** that allows sorting arrays. Doing a simple `array.sort()` will treat each array entry as a string and sort it alphabetically. Also you can provide your [own custom sorting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort#Parameters) function.

```javascript
['Shanghai', 'New York', 'Mumbai', 'Buenos Aires'].sort();
// ["Buenos Aires", "Mumbai", "New York", "Shanghai"]
```

But when you try order an array of non ASCII characters like this `['é', 'a', 'ú', 'c']`, you will obtain a strange result `['c', 'e', 'á', 'ú']`. That happens because sort works only with english language.

See the next example:

```javascript
// Spanish
['único','árbol', 'cosas', 'fútbol'].sort();
// ["cosas", "fútbol", "árbol", "único"] // bad order

// German
['Woche', 'wöchentlich', 'wäre', 'Wann'].sort();
// ["Wann", "Woche", "wäre", "wöchentlich"] // bad order
```

Fortunately, there are two ways to overcome this behavior [localeCompare](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare) and [Intl.Collator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Collator) provided by ECMAScript Internationalization API.

> Both methods have their own custom parameters in order to configure it to work adequately.

### Using `localeCompare()`

```javascript
['único','árbol', 'cosas', 'fútbol'].sort(function (a, b) {
  return a.localeCompare(b);
});
// ["árbol", "cosas", "fútbol", "único"]

['Woche', 'wöchentlich', 'wäre', 'Wann'].sort(function (a, b) {
  return a.localeCompare(b);
});
// ["Wann", "wäre", "Woche", "wöchentlich"]
```

### Using `Intl.Collator()`

```javascript
['único','árbol', 'cosas', 'fútbol'].sort(Intl.Collator().compare);
// ["árbol", "cosas", "fútbol", "único"]

['Woche', 'wöchentlich', 'wäre', 'Wann'].sort(Intl.Collator().compare);
// ["Wann", "wäre", "Woche", "wöchentlich"]
```

- For each method you can customize the location.
- According to [Firefox](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare#Performance) Intl.Collator is faster when comparing large numbers of strings.

So when you are working with arrays of strings in a language other than English, remember to use this method to avoid unexpected sorting.

## #03 - Improve Nested Conditionals
> 2016-01-03 by [AlbertoFuente](https://github.com/AlbertoFuente)

How can we improve and make more efficient nested `if` statement in javascript.

```javascript
if (color) {
  if (color === 'black') {
    printBlackBackground();
  } else if (color === 'red') {
    printRedBackground();
  } else if (color === 'blue') {
    printBlueBackground();
  } else if (color === 'green') {
    printGreenBackground();
  } else {
    printYellowBackground();
  }
}
```

One way to improve the nested `if` statement would be using the `switch` statement. Although it is less verbose and is more ordered, It's not recommended to use it because it's so difficult to debug errors, here's [why](https://toddmotto.com/deprecating-the-switch-statement-for-object-literals/).

```javascript
switch(color) {
  case 'black':
    printBlackBackground();
    break;
  case 'red':
    printRedBackground();
    break;
  case 'blue':
    printBlueBackground();
    break;
  case 'green':
    printGreenBackground();
    break;
  default:
    printYellowBackground();
}
```

But what if we have a conditional with several checks in each statement? In this case, if we like to do less verbose and more ordered, we can use the conditional `switch`.
If we pass `true` as parameter to the `switch` statement, It allows us to put a conditional in each case.

```javascript
switch(true) {
  case (typeof color === 'string' && color === 'black'):
    printBlackBackground();
    break;
  case (typeof color === 'string' && color === 'red'):
    printRedBackground();
    break;
  case (typeof color === 'string' && color === 'blue'):
    printBlueBackground();
    break;
  case (typeof color === 'string' && color === 'green'):
    printGreenBackground();
    break;
  case (typeof color === 'string' && color === 'yellow'):
    printYellowBackground();
    break;
}
```

But we must always avoid having several checks in every condition, avoiding use of `switch` as far as possible and take into account that the most efficient way to do this is through an `object`.

```javascript
var colorObj = {
  'black': printBlackBackground,
  'red': printRedBackground,
  'blue': printBlueBackground,
  'green': printGreenBackground,
  'yellow': printYellowBackground
};

if (color && colorObj.hasOwnProperty(color)) {
  colorObj[color]();
}
```

Here you can find more information about [this](http://www.nicoespeon.com/en/2015/01/oop-revisited-switch-in-js/).

## #02 - ReactJs - Keys in children components are important

> 2016-01-02  by [@loverajoel](https://twitter.com/loverajoel)


The [key](https://facebook.github.io/react/docs/multiple-components.html#dynamic-children) is an attribute that you must pass to all components created dynamically from an array. It's unique and constant id that React use for identify each component in the DOM and know that it's a different component and not the same one. Using keys will ensure that the child component is preserved and not recreated and prevent that weird things happens.

> Key is not really about performance, it's more about identity (which in turn leads to better performance). randomly assigned and changing values are not identity [Paul O’Shannessy](https://github.com/facebook/react/issues/1342#issuecomment-39230939)

- Use an existing unique value of the object.
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
- [Using array index is a bad practice.](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318#.76co046o9)
- `random()` will not work

	```javascript
	//bad
	<MyComponent key={{Math.random()}}/>
	```

- You can create your own unique id, be sure that the method be fast and attach it to your object.
- When the amount of child are big or involve expensive components, use keys has performance improvements.
- [You must provide the key attribute for all children of ReactCSSTransitionGroup.](http://docs.reactjs-china.com/react/docs/animation.html)

## #1 - AngularJs: `$digest` vs `$apply`

> 2016-01-01  by [@loverajoel](https://twitter.com/loverajoel)

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


## #0 - Insert item inside an Array
> 2015-12-29

Inserting an item into an existing array is a daily common task. You can add elements to the end of an array using push, to the beginning using unshift, or the middle using splice.

But those are known methods, doesn't mean there isn't a more performant way, here we go...

Adding an element at the end of the array is easy with push(), but there is a way more performant.

```javascript
var arr = [1,2,3,4,5];

arr.push(6);
arr[arr.length] = 6; // 43% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
Both methods modify the original array. Don't believe me? Check the [jsperf](http://jsperf.com/push-item-inside-an-array)

Now we are trying to add an item to the beginning of the array

```javascript
var arr = [1,2,3,4,5];

arr.unshift(0);
[0].concat(arr); // 98% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
Here is a little bit detail, unshift edits the original array, concat returns a new array. [jsperf](http://jsperf.com/unshift-item-inside-an-array)

Adding items at the middle of an array is easy with splice and is the most performant way to do it.

```javascript
var items = ['one', 'two', 'three', 'four'];
items.splice(items.length / 2, 0, 'hello');
```

I tried to run these tests in various Browsers and OS and the results were similar. I hope these tips will be useful for you and encourage to perform your own tests!

### License
[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png)](http://creativecommons.org/publicdomain/zero/1.0/)
