![header](https://raw.githubusercontent.com/loverajoel/jstips/gh-pages/resources/jstips-header-blog.gif)

# Introducing JavaScript Tips [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)
> New year, new project. **A JS tip per day!**

With great excitement, I introduce these short and useful daily JavaScript tips that will allow you to improve your code writing. With less than 2 minutes each day, you will be able to read about performance, conventions, hacks, interview questions and all the items that the future of this awesome language holds for us.

At midday, no matter if it is a weekend or a holiday, a tip will be posted and tweeted.

### Can you help us enrich it?
Please feel free to send us a PR with your own JavaScript tip to be published here.
Any improvements or suggestions are more than welcome!
[Click to see the instructions](https://github.com/loverajoel/jstips/blob/gh-pages/CONTRIBUTING.md)

### Let’s keep in touch

There are a lot of way to get update, choose your own

- [Official Blog](http://www.jstips.co)
- [Official Twitter Account](https://twitter.com/tips_js)
- [Hubot](https://github.com/dggriffin/hubot-jstips)
- [js2016.tips](http://js2016.tips/)
- [Hingsir](http://hingsir.com/jstips-site/dist/tips/)
- [Awesomelists](https://awesomelists.top/#/repos/loverajoel/jstips)

> Don't forget to Star the repo, as this will help to promote the project!

# Tips List

- [27-Short circuit evaluation in JS.](#27-short-circuit-evaluation-in-js)
- [26-Filtering and Sorting a List of Strings](#26-filtering-and-sorting-a-list-of-strings)
- [25-Using immediately invoked function expression](#25-using-immediately-invoked-function-expression)
- [24-Use === instead of ==](#24-use--instead-of-)
- [23-Converting to number fast way](#23-converting-to-number-fast-way)
- [22-Two ways to empty an array](#22-two-ways-to-empty-an-array)
- [21-Shuffle an Array](#21-shuffle-an-array)
- [20-Return objects to enable chaining of functions](#20-return-objects-to-enable-chaining-of-functions)
- [19-Safe string concatenation](#19-safe-string-concatenation)
- [18-Rounding the fast way](#18-rounding-the-fast-way)
- [17-Node.js - Run a module if it is not `required`](#17-nodejs-run-a-module-if-it-is-not-required)
- [16-Passing arguments to callback functions](#16-passing-arguments-to-callback-functions)
- [15-Even simpler way of using `indexOf` as a contains clause](#15-even-simpler-way-of-using-indexof-as-a-contains-clause)
- [14-Fat Arrow Functions](#14-fat-arrow-functions)
- [13-Tip to measure performance of a javascript block](#13-tip-to-measure-performance-of-a-javascript-block)
- [12-Pseudomandatory parameters in ES6 functions](#12-pseudomandatory-parameters-in-es6-functions)
- [11-Hoisting](#11-hoisting)
- [10-Check if a property is in a Object](#10-check-if-a-property-is-in-a-object)
- [09-Template Strings](#09-template-strings)
- [08-Converting a Node List to an Array](#08-converting-a-node-list-to-an-array)
- [07-use strict and get lazy](#07-use-strict-and-get-lazy)
- [06-Writing a single method for arrays and a single element](#06-writing-a-single-method-for-arrays-and-a-single-element)
- [05-Differences between `undefined` and `null`](#05-differences-between-undefined-and-null)
- [04-Sorting strings with accented characters](#04-sorting-strings-with-accented-characters)
- [03-Improve Nested Conditionals](#03-improve-nested-conditionals)
- [02-Keys in children components are important](#02-keys-in-children-components-are-important)
- [01-AngularJs - `$digest` vs `$apply`](#01-angularjs-digest-vs-apply)
- [00-Insert item inside an Array](#00-insert-item-inside-an-array)

### 27-Short circuit evaluation in JS.

[Short-circuit evaluation](https://en.wikipedia.org/wiki/Short-circuit_evaluation) says, the second argument is executed or evaluated only if the first argument does not suffice to determine the value of the expression: when the first argument of the AND (`&&`) function evaluates to false, the overall value must be false; and when the first argument of the OR (`||`) function evaluates to true, the overall value must be true.

For the following `test` condition and `isTrue` and `isFalse` function.

```js
var test = true;
var isTrue = function(){
  console.log('Test is true.');
};
var isFalse = function(){
  console.log('Test is false.');
};

```
Using logical AND - `&&`.

```js
// A normal if statement.
if(test){
  isTrue();    // Test is true
}

// Above can be done using '&&' as -

( test && isTrue() );  // Test is true
```
Using logical OR - `||`.

```js
test = false;
if(!test){
  isFalse();    // Test is false.
}

( test || isFalse());  // Test is false.
```
The logical OR could also be used to set a default value for function argument.

```js
function theSameOldFoo(name){
    name = name || 'Bar' ;
    console.log("My best friend's name is " + name);
}
theSameOldFoo();  // My best friend's name is Bar
theSameOldFoo('Bhaskar');  // My best friend's name is Bhaskar
```
The logical AND could be used to avoid exceptions when using properties of undefined.
Example:-

```js
var dog = {
  bark: function(){
     console.log('Woof Woof');
   }
};

// Calling dog.bark();
dog.bark(); // Woof Woof.

//But if dog is not defined, dog.bark() will raise an error "Cannot read property 'bark' of undefined."
// To prevent this, we can you &&.

dog&&dog.bark();   // This will only call dog.bark(), if dog is defined.

```

[⬆ To The Top](#tips-list)

### 26-Filtering and Sorting a List of Strings

You may have a big list of names you need to filter in order to remove duplicates and sort them alphabetically.

In our example we are going to use the list of **JavaScript reserved keywords** we can find across the different versions of the language, but as you can notice, there is a lot of duplicated keywords and they are not alphabetically organized. So this is a perfect list ([Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)) of strings to test out this JavaScript tip.

```js
var keywords = ['do', 'if', 'in', 'for', 'new', 'try', 'var', 'case', 'else', 'enum', 'null', 'this', 'true', 'void', 'with', 'break', 'catch', 'class', 'const', 'false', 'super', 'throw', 'while', 'delete', 'export', 'import', 'return', 'switch', 'typeof', 'default', 'extends', 'finally', 'continue', 'debugger', 'function', 'do', 'if', 'in', 'for', 'int', 'new', 'try', 'var', 'byte', 'case', 'char', 'else', 'enum', 'goto', 'long', 'null', 'this', 'true', 'void', 'with', 'break', 'catch', 'class', 'const', 'false', 'final', 'float', 'short', 'super', 'throw', 'while', 'delete', 'double', 'export', 'import', 'native', 'public', 'return', 'static', 'switch', 'throws', 'typeof', 'boolean', 'default', 'extends', 'finally', 'package', 'private', 'abstract', 'continue', 'debugger', 'function', 'volatile', 'interface', 'protected', 'transient', 'implements', 'instanceof', 'synchronized', 'do', 'if', 'in', 'for', 'let', 'new', 'try', 'var', 'case', 'else', 'enum', 'eval', 'null', 'this', 'true', 'void', 'with', 'break', 'catch', 'class', 'const', 'false', 'super', 'throw', 'while', 'yield', 'delete', 'export', 'import', 'public', 'return', 'static', 'switch', 'typeof', 'default', 'extends', 'finally', 'package', 'private', 'continue', 'debugger', 'function', 'arguments', 'interface', 'protected', 'implements', 'instanceof', 'do', 'if', 'in', 'for', 'let', 'new', 'try', 'var', 'case', 'else', 'enum', 'eval', 'null', 'this', 'true', 'void', 'with', 'await', 'break', 'catch', 'class', 'const', 'false', 'super', 'throw', 'while', 'yield', 'delete', 'export', 'import', 'public', 'return', 'static', 'switch', 'typeof', 'default', 'extends', 'finally', 'package', 'private', 'continue', 'debugger', 'function', 'arguments', 'interface', 'protected', 'implements', 'instanceof'];
```

Since we don't want to change our original list, we are going to use a high order function named [`filter`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/filter), which will return a new filter array based in a predicate (*function*) we pass to it. The predicate will compare the index of the current keyword in the original list with its `index` in the new list and will push it to the new array only if the indexes match.

Finally we are going to sort the filtered list using the [`sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) function which takes a comparison function as the only argument, returning a alphabetically sorted list.

```js
var filteredAndSortedKeywords = keywords
  .filter(function (keyword, index) {
      return keywords.indexOf(keyword) === index;
    })
  .sort(function (a, b) {
      if (a < b) return -1;
      else if (a > b) return 1;
      return 0;
    });
```

The **ES6** (ECMAScript 2015) version using [arrow functions](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions) looks a little simpler:

```js
const filteredAndSortedKeywords = keywords
  .filter((keyword, index) => keywords.indexOf(keyword) === index)
  .sort((a, b) => {
      if (a < b) return -1;
      else if (a > b) return 1;
      return 0;
    });
```

And this is the final filtered and sorted list of JavaScript reserved keywords:

```js
console.log(filteredAndSortedKeywords);

// ['abstract', 'arguments', 'await', 'boolean', 'break', 'byte', 'case', 'catch', 'char', 'class', 'const', 'continue', 'debugger', 'default', 'delete', 'do', 'double', 'else', 'enum', 'eval', 'export', 'extends', 'false', 'final', 'finally', 'float', 'for', 'function', 'goto', 'if', 'implements', 'import', 'in', 'instanceof', 'int', 'interface', 'let', 'long', 'native', 'new', 'null', 'package', 'private', 'protected', 'public', 'return', 'short', 'static', 'super', 'switch', 'synchronized', 'this', 'throw', 'throws', 'transient', 'true', 'try', 'typeof', 'var', 'void', 'volatile', 'while', 'with', 'yield']
```

[⬆ To The Top](#tips-list)

### 25-Using immediately invoked function expression

Called as "Iffy" ( IIFE - immediately invoked function expression) is an anonymous function expression that is immediately invoked and has some important uses in Javascript.

```javascript

(function() {
 // Do something​
 }
)()

```

It is an anonymous function expression that is immediately invoked, and it has some particularly important uses in JavaScript.

The pair of parenthesis surrounding the anonymous function turns the anonymous function into a function expression or variable expression. So instead of a simple anonymous function in the global scope, or wherever it was defined, we now have an unnamed function expression.

Similarly, we can even create a named, immediately invoked function expression:

```javascript
(someNamedFunction = function(msg) {
	console.log(msg || "Nothing for today !!")
	}) (); // Output --> Nothing for today !!​
​
someNamedFunction("Javascript rocks !!"); // Output --> Javascript rocks !!
someNamedFunction(); // Output --> Nothing for today !!​
```

For more details, check the following URL's -
1. [Link 1](https://blog.mariusschulz.com/2016/01/13/disassembling-javascripts-iife-syntax)
2. [Link 2](http://javascriptissexy.com/12-simple-yet-powerful-javascript-tips/)

Performance:
[jsPerf](http://jsperf.com/iife-with-call)

[⬆ To The Top](#tips-list)

### 24-Use === instead of ==

The `==` (or `!=`) operator performs an automatic type conversion if needed. The `===` (or `!==`) operator will not perform any conversion. It compares the value and the type, which could be considered faster ([jsPref](http://jsperf.com/strictcompare)) than `==`.

```js
[10] ==  10      // is true
[10] === 10      // is false

'10' ==  10      // is true
'10' === 10      // is false

 []  ==  0       // is true
 []  === 0       // is false

 ''  ==  false   // is true but true == "a" is false
 ''  === false   // is false

```

[⬆ To The Top](#tips-list)

### 23-Converting to number fast way

Converting strings to numbers is extremely common. The easiest and fastest ([jsPref](https://jsperf.com/number-vs-parseint-vs-plus/29)) way to achieve that would be using the `+` (plus) operator.

```javascript
var one = '1';

var numberOne = +one; // Number 1
```

You can also use the `-` (minus) operator which type-converts the value into number but also negates it.

```javascript
var one = '1';

var negativeNumberOne = -one; // Number -1
```

[⬆ To The Top](#tips-list)

### 22-Two ways to empty an array

You define an array and want to empty its contents.
Usually, you would do it like this:

```javascript
// define Array
var list = [1, 2, 3, 4];
function empty() {
    //empty your array
    list = [];
}
empty();
```
But there is another way to empty an array that is more performant.

You should use code like this:

```javascript
var list = [1, 2, 3, 4];
function empty() {
    //empty your array
    list.length = 0;
}
empty();
```

* `list = []` assigns a reference to a new array to a variable, while any other references are unaffected.
which means that references to the contents of the previous array are still kept in memory, leading to memory leaks.

* `list.length = 0` deletes everything in the array, which does hit other references.

In other words, if you have two references to the same array (`a = [1,2,3]; a2 = a;`), and you delete the array's contents using `list.length = 0`, both references (a and a2) will now point to the same empty array. (So don't use this technique if you don't want a2 to hold an empty array!)

Think about what this will output:

```js
var foo = [1,2,3];
var bar = [1,2,3];
var foo2 = foo;
var bar2 = bar;
foo = [];
bar.length = 0;
console.log(foo, bar, foo2, bar2);

// [] [] [1, 2, 3] []
```

Stackoverflow more detail:
[difference-between-array-length-0-and-array](http://stackoverflow.com/questions/4804235/difference-between-array-length-0-and-array)

[⬆ To The Top](#tips-list)

### 21-Shuffle an Array

This snippet here uses [Fisher-Yates Shuffling](https://www.wikiwand.com/en/Fisher%E2%80%93Yates_shuffle) Algorithm to shuffle a given array.

```javascript
function shuffle(arr) {
    var i,
        j,
        temp;
    for (i = arr.length - 1; i > 0; i--) {
        j = Math.floor(Math.random() * (i + 1));
        temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
    return arr;    
};
```
An example:

```javascript
var a = [1, 2, 3, 4, 5, 6, 7, 8];
var b = shuffle(a);
console.log(b);
// [2, 7, 8, 6, 5, 3, 1, 4]
```

[⬆ To The Top](#tips-list)

### 20-Return objects to enable chaining of functions

When creating functions on an object in Object Oriented Javascript, returning the object in the function will enable you to chain functions together.

```js
function Person(name) {
  this.name = name;

  this.sayName = function() {
    console.log("Hello my name is: ", this.name);
    return this;
  };

  this.changeName = function(name) {
    this.name = name;
    return this;
  };
}

var person = new Person("John");
person.sayName().changeName("Timmy").sayName();
```

[⬆ To The Top](#tips-list)

### 19-Safe string concatenation

Suppose you have a couple of variables with unknown types and you want to concatenate them in a string. To be sure that the arithmetical operation is not be applied during concatenation, use `concat`:

```javascript
var one = 1;
var two = 2;
var three = '3';

var result = ''.concat(one, two, three); //"123"
```

This way of concatenting does exactly what you'd expect. In contrast, concatenation with pluses might lead to unexpected results:

```javascript
var one = 1;
var two = 2;
var three = '3';

var result = one + two + three; //"33" instead of "123"
```

Speaking about performance, compared to the `join` [type](http://www.sitepoint.com/javascript-fast-string-concatenation/) of concatenation, the speed of `concat` is pretty much the same.

You can read more about the `concat` function on MDN [page](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/concat).

[⬆ To The Top](#tips-list)

### 18-Rounding the fast way

Today's tip is about performance. [Ever came across the double tilde] (http://stackoverflow.com/questions/5971645/what-is-the-double-tilde-operator-in-javascript) `~~` operator? It is sometimes also called the double NOT bitwise operator. You can use it as a faster substitute for `Math.floor()`. Why is that?

One bitwise shift `~` transforms the 32 bit converted input into `-(input+1)`. The double bitwise shift therefore transforms the input into `-(-(input + 1)+1)` making it a great tool to round towards 0. For numeric input, it therefore mimics the `Math.ceil()` for negative and `Math.floor()` for positive input. On failure, `0` is returned, which might come in handy sometimes instead of `Math.floor()`, which returns a value of `NaN` on failure.

```javascript
// single ~
console.log(~1337)    // -1338

// numeric input
console.log(~~47.11)  // -> 47
console.log(~~-12.88) // -> -12
console.log(~~1.9999) // -> 1
console.log(~~3)      // -> 3

// on failure
console.log(~~[]) // -> 0
console.log(~~NaN)  // -> 0
console.log(~~null) // -> 0

// greater than 32 bit integer fails
console.log(~~(2147483647 + 1) === (2147483647 + 1)) // -> 0
```

Although `~~` may perform better, for the sake of readability please use `Math.floor()`.

[⬆ To The Top](#tips-list)

### 17-Node.js - Run a module if it is not `required`

In node, you can tell your program to do two different things depending on whether the code is run from `require('./something.js')` or `node something.js`.  This is useful if you want to interact with one of your modules independently.

```js
if (!module.parent) {
    // ran with `node something.js`
    app.listen(8088, function() {
        console.log('app listening on port 8088');
    })
} else {
    // used with `require('/.something.js')`
    module.exports = app;
}
```

See [the documentation for modules](https://nodejs.org/api/modules.html#modules_module_parent) for more info.

[⬆ To The Top](#tips-list)

### 16-Passing arguments to callback functions

By default you cannot pass arguments to a callback function. For example:

```js
function callback() {
  console.log('Hi human');
}

document.getElementById('someelem').addEventListener('click', callback);

```

You can take advantage of the closure scope in Javascript to pass arguments to callback functions. Check this example:

```js
function callback(a, b) {
  return function() {
    console.log('sum = ', (a+b));
  }
}

var x = 1, y = 2;
document.getElementById('someelem').addEventListener('click', callback(x, y));

```

### What are closures?

Closures are functions that refer to independent (free) variables. In other words, the function defined in the closure 'remembers' the environment in which it was created. [Check MDN Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) to learn more.

So this way the arguments `x` and `y` are in scope of the callback function when it is called.

Another method to do this is using the `bind` method. For example:

```js
var alertText = function(text) {
  alert(text);
};

document.getElementById('someelem').addEventListener('click', alertText.bind(this, 'hello'));
```
There is a very slight difference in performance of both methods, checkout [jsperf](http://jsperf.com/bind-vs-closure-23).

[⬆ To The Top](#tips-list)

### 15-Even simpler way of using `indexOf` as a contains clause

JavaScript by default does not have a contains method. And for checking existence of a substring in a string or an item in an array you may do this:

```javascript
var someText = 'javascript rules';
if (someText.indexOf('javascript') !== -1) {
}

// or
if (someText.indexOf('javascript') >= 0) {
}
```

But let's look at these [Expressjs](https://github.com/strongloop/express) code snippets.

[examples/mvc/lib/boot.js](https://github.com/strongloop/express/blob/2f8ac6726fa20ab5b4a05c112c886752868ac8ce/examples/mvc/lib/boot.js#L26)


```javascript
for (var key in obj) {
  // "reserved" exports
  if (~['name', 'prefix', 'engine', 'before'].indexOf(key)) continue;
```

[lib/utils.js](https://github.com/strongloop/express/blob/2f8ac6726fa20ab5b4a05c112c886752868ac8ce/lib/utils.js#L93)


```javascript
exports.normalizeType = function(type){
  return ~type.indexOf('/')
    ? acceptParams(type)
    : { value: mime.lookup(type), params: {} };
};
```

[examples/web-service/index.js](https://github.com/strongloop/express/blob/2f8ac6726fa20ab5b4a05c112c886752868ac8ce/examples/web-service/index.js#L35)


```javascript
// key is invalid
if (!~apiKeys.indexOf(key)) return next(error(401, 'invalid api key'));
```

The gotcha is the [bitwise operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators) **~**, "Bitwise operators perform their operations on binary representations, but they return standard JavaScript numerical values."

It transforms `-1` into `0`, and `0` evaluates to `false` in JavaScript:

```javascript
var someText = 'text';
!!~someText.indexOf('tex'); // someText contains "tex" - true
!~someText.indexOf('tex'); // someText NOT contains "tex" - false
~someText.indexOf('asd'); // someText doesn't contain "asd" - false
~someText.indexOf('ext'); // someText contains "ext" - true
```

### String.prototype.includes()

ES6 introduced the [includes() method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes) and you can use it to determine whether or not a string includes another string:

```javascript
'something'.includes('thing'); // true
```

With ECMAScript 2016 (ES7) it is even possible to use these techniques with Arrays:

```javascript
!!~[1, 2, 3].indexOf(1); // true
[1, 2, 3].includes(1); // true
```

**Unfortunately, it is only supported in Chrome, Firefox, Safari 9 or above and Edge; not IE11 or lower.**
**It's better used in controlled environments.**

[⬆ To The Top](#tips-list)

### 14-Fat Arrow Functions

Introduced as a new feature in ES6, fat arrow functions may come as a handy tool to write more code in fewer lines. The name comes from its syntax, `=>`, which is a 'fat arrow', as compared to a thin arrow `->`. Some programmers might already know this type of function from different languages such as Haskell, as 'lambda expressions', or as 'anonymous functions'. It is called anonymous, as these arrow functions do not have a descriptive function name.

### What are the benefits?
* Syntax: fewer LOC; no more typing `function` keyword over and over again
* Semantics: capturing the keyword `this` from the surrounding context

### Simple syntax example
Have a look at these two code snippets, which do the exact same job, and you will quickly understand what fat arrow functions do:

```javascript
// general syntax for fat arrow functions
param => expression

// may also be written with parentheses
// parentheses are required on multiple params
(param1 [, param2]) => expression


// using functions
var arr = [5,3,2,9,1];
var arrFunc = arr.map(function(x) {
  return x * x;
});
console.log(arr)

// using fat arrow
var arr = [5,3,2,9,1];
var arrFunc = arr.map((x) => x*x);
console.log(arr)
```

As you can see, the fat arrow function in this case can save you time typing out the parentheses as well as the function and return keywords. I would advise you to always write parentheses around the parameter inputs, as the parentheses will be needed for multiple input parameters, such as in `(x,y) => x+y`. It is just a way to cope with forgetting them in different use cases. But the code above would also work like this: `x => x*x`. So far, these are only syntactical improvements, which lead to fewer LOC and better readability.

### Lexically binding `this`

There is another good reason to use fat arrow functions. There is the issue with the context of `this`. With arrow functions, you don't need to worry about `.bind(this)` or setting `that = this` anymore, as fat arrow functions pick the context of `this` from the lexical surrounding. Have a look at the next [example] (https://jsfiddle.net/pklinger/rw94oc11/):

```javascript

// globally defined this.i
this.i = 100;

var counterA = new CounterA();
var counterB = new CounterB();
var counterC = new CounterC();
var counterD = new CounterD();

// bad example
function CounterA() {
  // CounterA's `this` instance (!! gets ignored here)
  this.i = 0;
  setInterval(function () {
    // `this` refers to global object, not to CounterA's `this`
    // therefore starts counting with 100, not with 0 (local this.i)
    this.i++;
    document.getElementById("counterA").innerHTML = this.i;
  }, 500);
}

// manually binding that = this
function CounterB() {
  this.i = 0;
  var that = this;
  setInterval(function() {
    that.i++;
    document.getElementById("counterB").innerHTML = that.i;
  }, 500);
}

// using .bind(this)
function CounterC() {
  this.i = 0;
  setInterval(function() {
    this.i++;
    document.getElementById("counterC").innerHTML = this.i;
  }.bind(this), 500);
}

// fat arrow function
function CounterD() {
  this.i = 0;
  setInterval(() => {
    this.i++;
    document.getElementById("counterD").innerHTML = this.i;
  }, 500);
}
```

Further information about fat arrow functions may be found at [MDN] (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions). To see different syntax options visit [this site] (http://jsrocks.org/2014/10/arrow-functions-and-their-scope/).

[⬆ To The Top](#tips-list)

### 13-Tip to measure performance of a javascript block

For quickly measuring performance of a javascript block, we can use the console functions like
[`console.time(label)`](https://developer.chrome.com/devtools/docs/console-api#consoletimelabel) and [`console.timeEnd(label)`](https://developer.chrome.com/devtools/docs/console-api#consoletimeendlabel)

```javascript
console.time("Array initialize");
var arr = new Array(100),
    len = arr.length,
    i;

for (i = 0; i < len; i++) {
    arr[i] = new Object();
};
console.timeEnd("Array initialize"); // Outputs: Array initialize: 0.711ms
```

More info:
[Console object](https://github.com/DeveloperToolsWG/console-object),
[Javascript benchmarking](https://mathiasbynens.be/notes/javascript-benchmarking)

Demo: [jsfiddle](https://jsfiddle.net/meottb62/) - [codepen](http://codepen.io/anon/pen/JGJPoa) (outputs in browser console)

[⬆ To The Top](#tips-list)

### 12-Pseudomandatory parameters in ES6 functions

In many programming languages the parameters of a function are by default mandatory and the developer has to explicitly define that a parameter is optional. In Javascript, every parameter is optional, but we can enforce this behavior without messing with the actual body of a function, taking advantage of [**es6's default values for parameters**] (http://exploringjs.com/es6/ch_parameter-handling.html#sec_parameter-default-values) feature.

```javascript
const _err = function( message ){
  throw new Error( message );
}

const getSum = (a = _err('a is not defined'), b = _err('b is not defined')) => a + b

getSum( 10 ) // throws Error, b is not defined
getSum( undefined, 10 ) // throws Error, a is not defined
 ```

 `_err` is a function that immediately throws an Error. If no value is passed for one of the parameters, the default value is going to be used, `_err` will be called and an Error will be thrown. You can see more examples for the **default parameters feature** on [Mozilla's Developer Network ](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/default_parameters)

[⬆ To The Top](#tips-list)

### 11-Hoisting

Understanding [hoisting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var#var_hoisting) will help you organize your function scope. Just remember, variable declarations and function definitions are hoisted to the top. Variable definitions are not, even if you declare and define a variable on the same line. Also, a variable **declaration** lets the system know that the variable exists while **definition** assigns it a value.

```javascript
function doTheThing() {
  // ReferenceError: notDeclared is not defined
  console.log(notDeclared);

  // Outputs: undefined
  console.log(definedLater);
  var definedLater;

  definedLater = 'I am defined!'
  // Outputs: 'I am defined!'
  console.log(definedLater)

  // Outputs: undefined
  console.log(definedSimulateneously);
  var definedSimulateneously = 'I am defined!'
  // Outputs: 'I am defined!'
  console.log(definedSimulateneously)

  // Outputs: 'I did it!'
  doSomethingElse();

  function doSomethingElse(){
    console.log('I did it!');
  }

  // TypeError: undefined is not a function
  functionVar();

  var functionVar = function(){
    console.log('I did it!');
  }
}
```

To make things easier to read, declare all of your variables at the top of your function scope so it is clear which scope the variables are coming from. Define your variables before you need to use them. Define your functions at the bottom of your scope to keep them out of your way.

[⬆ To The Top](#tips-list)

### 10-Check if a property is in a Object

When you have to check if a property is present in an [object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects), you probably are doing something like this:

```javascript
var myObject = {
  name: '@tips_js'
};

if (myObject.name) { ... }

```

That's ok, but you have to know that there are two native ways for this kind of thing, the [`in` operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in) and [`Object.hasOwnProperty`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty). Every object descended from `Object`, has both ways available.

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

Both differ in the depth at which they check the properties. In other words, `hasOwnProperty` will only return true if key is available on that object directly. However, the `in` operator doesn't discriminate between properties created on an object and properties inherited from the prototype chain.

Here's another example:

```javascript
var myFunc = function() {
  this.name = '@tips_js';
};
myFunc.prototype.age = '10 days';

var user = new myFunc();

user.hasOwnProperty('name'); // true
user.hasOwnProperty('age'); // false, because age is from the prototype chain
```

Check the [live examples here](https://jsbin.com/tecoqa/edit?js,console)!

I also recommend reading [this discussion](https://github.com/loverajoel/jstips/issues/62) about common mistakes made when checking a property's existence in objects.

[⬆ To The Top](#tips-list)

### 09-Template Strings

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

You can do multi-line strings without `\n` and simple logic (ie 2+3) inside `${}` in template strings.

You are also able to to modify the output of template strings using a function; they are called [tagged template strings]
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings#Tagged_template_strings) for example usages of tagged template strings.

You may also want to [read](https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2) to understand template strings more.

[⬆ To The Top](#tips-list)

### 08-Converting a Node List to an Array

The `querySelectorAll` method returns an array-like object called a node list. These data structures are referred to as "Array-like", because they appear as an array, but can not be used with array methods like `map` and `forEach`. Here's a quick, safe, and reusable way to convert a node list into an array of DOM elements:

```javascript
const nodelist = document.querySelectorAll('div');
const nodelistToArray = Array.apply(null, nodelist);

//later on ..

nodelistToArray.forEach(...);
nodelistToArray.map(...);
nodelistToArray.slice(...);

//etc...
```

The `apply` method is used to pass an array of arguments to a function with a given `this` value. [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) states that `apply` will take an array-like object, which is exactly what `querySelectorAll` returns. Since we don't need to specify a value for `this` in the context of the function, we pass in `null` or `0`. The result is an actual array of DOM elements which contains all of the available array methods.

Or if you are using ES2015 you can use the [spread operator `...`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)

```js
const nodelist = [...document.querySelectorAll('div')]; // returns a real array

//later on ..

nodelist.forEach(...);
nodelist.map(...);
nodelist.slice(...);

//etc...
```

[⬆ To The Top](#tips-list)

### 07-use strict and get lazy

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
* Attempting to write to read-only properties generates a noisy error
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

[⬆ To The Top](#tips-list)

### 06-Writing a single method for arrays and a single element

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

[⬆ To The Top](#tips-list)

### 05-Differences between `undefined` and `null`

- `undefined` means a variable has not been declared, or has been declared but has not yet been assigned a value
- `null` is an assignment value that means "no value"
- Javascript sets unassigned variables with a default value of `undefined`
- Javascript never sets a value to `null`. It is used by programmers to indicate that a `var` has no value.
- `undefined` is not valid in JSON while `null` is
- `undefined` typeof is `undefined`
- `null` typeof is an `object`. [Why?](http://www.2ality.com/2013/10/typeof-null.html)
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

[⬆ To The Top](#tips-list)

### 04-Sorting strings with accented characters

Javascript has a native method **[sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)** that allows sorting arrays. Doing a simple `array.sort()` will treat each array entry as a string and sort it alphabetically. Also you can provide your [own custom sorting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort#Parameters) function.

```javascript
['Shanghai', 'New York', 'Mumbai', 'Buenos Aires'].sort();
// ["Buenos Aires", "Mumbai", "New York", "Shanghai"]
```

But when you try order an array of non ASCII characters like this `['é', 'a', 'ú', 'c']`, you will obtain a strange result `['c', 'e', 'á', 'ú']`. That happens because sort works only with the English language.

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

[⬆ To The Top](#tips-list)

### 03-Improve Nested Conditionals

How can we improve and make a more efficient nested `if` statement in javascript?

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

One way to improve the nested `if` statement would be using the `switch` statement. Although it is less verbose and is more ordered, it's not recommended to use it because it's so difficult to debug errors. Here's [why](https://toddmotto.com/deprecating-the-switch-statement-for-object-literals/).

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

[⬆ To The Top](#tips-list)

### 02-Keys in children components are important

The [key](https://facebook.github.io/react/docs/multiple-components.html#dynamic-children) is an attribute that you must pass to all components created dynamically from an array. It's a unique and constant id that React uses to identify each component in the DOM and to know whether it's a different component or the same one. Using keys ensures that the child component is preserved and not recreated and prevents weird things from happening.

> Key is not really about performance, it's more about identity (which in turn leads to better performance). Randomly assigned and changing values do not form an identity [Paul O’Shannessy](https://github.com/facebook/react/issues/1342#issuecomment-39230939)

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

- You can create your own unique id. Be sure that the method is fast and attach it to your object.
- When the number of children is large or contains expensive components, use keys to improve performance.
- [You must provide the key attribute for all children of ReactCSSTransitionGroup.](http://docs.reactjs-china.com/react/docs/animation.html)

[⬆ To The Top](#tips-list)

### 01-AngularJs - `$digest` vs `$apply`

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
- If you are using >AngularJS 1.2.X, use `$evalAsync`, which is a core method that will evaluate the expression during the current cycle or the next. This can improve your application's performance.

[⬆ To The Top](#tips-list)

### 00-Insert item inside an Array

Inserting an item into an existing array is a daily common task. You can add elements to the end of an array using push, to the beginning using unshift, or to the middle using splice.

Those are known methods, but it doesn't mean there isn't a more performant way. Here we go:

Adding an element at the end of the array is easy with push(), but there is a more performant way.

```javascript
var arr = [1,2,3,4,5];

arr.push(6);
arr[arr.length] = 6; // 43% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
Both methods modify the original array. Don't believe me? Check the [jsperf](http://jsperf.com/push-item-inside-an-array)

Now if we are trying to add an item to the beginning of the array:

```javascript
var arr = [1,2,3,4,5];

arr.unshift(0);
[0].concat(arr); // 98% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
Here is a little more detail: unshift edits the original array; concat returns a new array. [jsperf](http://jsperf.com/unshift-item-inside-an-array)

Adding items in the middle of an array is easy with splice, and it's the most performant way to do it.

```javascript
var items = ['one', 'two', 'three', 'four'];
items.splice(items.length / 2, 0, 'hello');
```

I tried to run these tests in various Browsers and OS and the results were similar. I hope these tips will be useful for you and encourage to perform your own tests!

[⬆ To The Top](#tips-list)
