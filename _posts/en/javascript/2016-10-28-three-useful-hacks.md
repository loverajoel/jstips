---
layout: post

title: Three useful hacks
tip-number: 60
tip-username: leandrosimoes 
tip-username-profile: https://github.com/leandrosimoes
tip-tldr: Three very useful and syntax sugar hacks to speed up your development.


redirect_from:
  - /en/three-useful-hacks/

categories:
    - en
    - javascript
---

#### Getting array items from behind to front

If you want to get the array items from behind to front, just do this:

```javascript
var newArray = [1, 2, 3, 4];

console.log(newArray.slice(-1)); // [4]
console.log(newArray.slice(-2)); // [3, 4]
console.log(newArray.slice(-3)); // [2, 3, 4]
console.log(newArray.slice(-4)); // [1, 2, 3, 4]
```

#### Short-circuits conditionals

If you have to execute a function just if a condition is `true`, like this:

```javascript
if(condition){
    dosomething();
}
```

You can use a short-circuit just like this:

```javascript
condition && dosomething();
```


#### Set variable default values using "||"


If you have to set a default value to variables, you can simple do this:

```javascript
var a;

console.log(a); //undefined

a = a || 'default value';

console.log(a); //default value

a = a || 'new value';

console.log(a); //default value
```