---
layout: post

title: Three useful hacks
tip-number: 00
tip-username: leandrosimoes 
tip-username-profile: https://github.com/leandrosimoes
tip-tldr: Three very useful and sintax sugar hacks to speed up your development.


categories:
    - en
---

#### Convert to boolean using "!!"

Sometimes we need to verify if a variable is not `false, 0, "", undefined or NaN`, so a short way to do this is:

```javascript
var varWithoutValue;

console.log(!!varWithoutValue); // false

varWithoutValue = 'now has value';

console.log(!!varWithoutValue); // true
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