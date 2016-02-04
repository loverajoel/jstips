---
layout: post

title: Assignment Operators
tip-number: 35
tip-username: hsleonis
tip-username-profile: https://github.com/hsleonis
tip-tldr: Assigning is very common. Sometimes typing becomes time consuming for us 'Lazy programmers'. So, we can use some tricks to help us and make our code cleaner and simpler.

categories:
    - en
---

Assigning is very common. Sometimes typing becomes time consuming for us 'Lazy programmers'.
So, we can use some tricks to help us and make our code cleaner and simpler.

Instead of using:

````javascript
a = true;
b = false;
````
We can use:
````javascript
a |= 1;
b &= 0;
````
This is the similiar use of

````javascript
x += 23; // x = x + 23;
y -= 15; // y = y - 15;
z *= 10; // z = z * 10;
k /= 7; // k = k / 7;
p %= 3; // p = p % 3;
d **= 2; // d = d ** 2;
m >>= 2; // m = m >> 2;
n <<= 2; // n = n << 2;
n ++; // n = n + 1;
n --; n = n - 1;

````

#### If-else (Using ternary operator) ####

This is what we write on regular basis.

````javascript
var newValue;
if(value > 10) 
  newValue = 5;
else
  newValue = 2;
````

We can user ternary operator to make it awesome:

````javascript
var newValue = (value > 10) ? 5 : 2;
````

#### Null, Undefined, Empty Checks ####

````javascript
if (variable1 !== null || variable1 !== undefined || variable1 !== '') {
     var variable2 = variable1;
}
````

Shorthand here:

````javascript
var variable2 = variable1  || '';
````
P.S.: If variable1 is a number, then first check if it is 0.

#### Object Array Notation ####

Instead of using:

````javascript
var a = new Array();
a[0] = "myString1";
a[1] = "myString2";
````
Use this:

````javascript
var a = ["myString1", "myString2"];
````

#### Associative array ####

Instead of using:

````javascript
var skillSet = new Array();
skillSet['Document language'] = 'HTML5';
skillSet['Styling language'] = 'CSS3';
````

Use this:

````javascript
var skillSet = {
    'Document language' : 'HTML5', 
    'Styling language' : 'CSS3'
};
````
