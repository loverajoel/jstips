---
layout: post

title: Call apply and bind. and how they are different.
tip-number: 68
tip-username: munjalsagar 
tip-username-profile: https://github.com/sagarmunjal
tip-tldr: Call apply and Bind are few of the most important concepts which lay a good foundation for JS Ninja. 


categories:
    - en
    - javascript
---

# Call apply and bind. and how they are different. 

prerequisites. 

-function invocation
-execution context
-variable environment
-scope
-scope chain
-objects
-methods

**Call and Apply**

Call apply and bind are methods listed in `Prototype property` of `Function Object`. 

Using `Object.prototype` `hasOwnProperty()` method you can get a boolean value. 

`Object.prototype.hasOwnProperty()`

The above returns a boolean indicating whether an object contains the specified property as a direct property of that object and not inherited through the prototype chain.


```javascript=
Function.prototype.hasOwnProperty('call'); // true
Function.prototype.hasOwnProperty('apply'); // true
Function.prototype.hasOwnProperty('bind'); // true
```
We use call and apply interchangeably and soon we will also get to know the how the two differ. 
As we know that Objects have properties and methods. 

Call or Apply help us to manipulate the `context` of any method or function.

By use of Call or Apply we can chose a `context` of our choice. 

In other words you can also think of it as a method or a stand-alone-function given capability to extend functionality of another object.

We have defined a function `getName` and an object `o` with a property `name` in line 1 below. 

Function `getName` logs the value of `this.name` which equals to the name property of the object invoking that function. 

We use `apply` to invoke `getName` on the object `o`. We will discuss the difference between call and apply next. 

```javascript=
function getName(){console.log(this.name)}
var o = {name : "kafka"};
getName(); // undefined
getName.apply(o); // returns kafka
getName.call(o); // returns kafka
```


In the above example we had used the function `getName.apply(o)` and `getName.call(o)`. 

Both call and apply, expect the first argument to be the `Execution Context` i.e. the name of the `object` on which the function or method is being applied. 
```
functionName.call(executionCotext);
functionName.apply(executionCotext);
```



Earlier we defined a function `getName` and we used call and apply to use it on the object `o` which then  logged the name property of the object which was passed as the parameter. 

We have defined a new function `addAge` and `addProfession`. Both the functions expect an argument and those values are passed as `properties` to the `object`.

`addAge` accepts an argument `age` i.e. `Number` and `addProfession` expects an argument `profession` i.e. `String`.  
When we invoke the function on line 6-7 we pass the arguments as the second argument to the `apply` and `call` method. 

Call and apply both accept the first argument as the `execution context` and the following arguments are the arguments that have to be passed to the function `call` and `apply` respectively.

```
addAge.apply(o,[19]);  // 19 is the argument
addAge.profession(o,"JavaScriptNinja") // "JavaScriptNinja" is the argument
```

The small difference between call and apply is only that apply accepts its arguments in the form of an array and call accepts the arguments in the form of a comma separated list.  

Below we invoke `addAge` and `addProfession` using call and apply in line 6-7 and pass the respective arguments. The function `addAge` and `addProfession` add two more properties to the object `o`. 

```javascript=
function addAge(age){
    this.age = age;
    return this;
}
function addProfession(profession){
    this.profession = age;
    return this;
}
var o = {name : "kafka"};
addAge.apply(o,[19]);
addProfession.call(o,"JavaScriptNinja");


```


**Bind**


A bind function is basically which binds the context of something and then stores it into a variable for invocation at a later stage. 

Below we are again using the same example as mentioned above and on line 3 we are storing reference to the `o.name` in `variable` `objectName`.

Unlike, call and apply, bind helps us to first store reference in a variable (line 3). Invoke the function at a later stage in line 4. 
Also, it makes the code more readable. 

```javascript=
function getName(){console.log(this.name)}
var o = {name:"kafka"};
var objectName = getName.bind(o);
objectName();

```
