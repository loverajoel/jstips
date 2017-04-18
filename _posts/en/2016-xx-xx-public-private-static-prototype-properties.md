---
layout: post

title: Public, private, static and prototype properties in JS.
tip-number: xx
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: 
* Private properties are defined by using 'var' keyword inside the object, its not directly accessible to instances.
* Public properties are defined by using `this.propertyName`, it is accessible to instances.
* Prototype properties are defined by `Classname.prototype.propertyName`, its public and is shared by instances.
* Static properties are defined by `Classname.propertyName`, it can be used without creating instances.


categories:
    - en
---

This shows how to create public, private, static variables and methods in "classes" in Javascript's classical OOP patern through the rather simple example of a person.

**TL;DR**
* **private variables** are declared with the 'var' keyword inside the object, and can only be accessed by private functions and privileged methods.
* **private functions** are declared inline inside the object's constructor (or alternatively may be defined via ` var functionName=function(){...})` and may only be called by privileged methods (including the object's constructor).
* **privileged methods** are declared with this.methodName=function(){...} and may invoked by code external to the object.
* **public properties** are declared with this.variableName and may be read/written from outside the object.
* **public methods** are defined by `Classname.prototype.methodName = function(){...}` and may be called from outside the object.
* **prototype properties** are defined by `Classname.prototype.propertyName = someValue` and are shared by all object instances, but may be overridden.
* **static properties** are defined by `Classname.propertyName = someValue`.


Example:-

```javascript 
function Maths(x, y){
  
    // Public properties.
    this.x = x;
    this.y = y;
    
    // Public methods.
    this.add = function(){ _sum = x + y; return _sum; }
    
    // Private variables
    _sum = 0;
    
    // Private methods.
    function _showResult(){
      console.log( "sum: " + _sum );
    }
    
    // Public method calls public and private method
    this.show = function(){
      this.add();
        _showResult();
    };
}

// Prototype property, shared by instances.
Maths.prototype.pi = 3.141;

// Static method, can be used without creating instance.
Maths.multiply = function(x, y){ return x*y; }

var instance = new Maths(3, 4);    // Intentiating Maths function.
instance.show();    // Console logs "sum: 7".

console.log(instance.add());    // Console logs 7. 
console.log(instance.pi);    // Console logs 3.141.
console.log(instance.x);  //  Console logs 3.
console.log(instance._sum)  // Console logs undefined

var result = Maths.multiply(3, 4); 
console.log(result);    // Console logs 12.

var instance2 = new Maths(2, 3);
console.log(instance2.pi);    // Console logs 3.141. Since this is shared variable.

instance2.pi = 3.14159;  // This will create a new public property pi specific to instance2, which will override the prototype property for instance2.

console.log(instance2.pi); // Console logs 3.14159.

```
More detail: [OOP in JS](http://phrogz.net/JS/classes/OOPinJS.html)
.
