---
layout: post

title: Know the passing mechanism
tip-number: 44
tip-username: bmkmanoj
tip-username-profile: https://github.com/bmkmanoj
tip-tldr: JavaScript technically only passes by value for both primitives and object (or reference) types. In case of reference types the reference value itself is passed by value.

redirect_from:
  - /en/know-the-passing-mechanism/

categories:
    - en
    - javascript
---

JavaScript is pass-by-value, technically. It is neither pass-by-value nor pass-by-reference, going by the truest sense of these terms. To understand this passing mechanism, take a look at the following two example code snippets and the explanations.

### Example 1

```js

var me = {					// 1
	'partOf' : 'A Team'
}; 

function myTeam(me) {		// 2

	me = {					// 3
		'belongsTo' : 'A Group'
	}; 
} 	

myTeam(me);		
console.log(me);			// 4  : {'partOf' : 'A Team'}

```

In above example, when the `myTeam` gets invoked, JavaScript is *passing the reference to* `me` *object as value, as it is an object* and invocation itself creates two independent references to the same object, (though the name being same here i.e. `me`, is misleading and gives us an impression that it is the single reference) and hence, the reference variable themselves are independent.

When we assigned a new object at #`3`, we are changing this reference value entirely within the `myTeam` function, and it will not have any impact on the original object outside this function scope, from where it was passed and the reference in the outside scope is going to retain the original object and hence the output from #`4`. 


### Example 2

```js

var me = {					// 1
	'partOf' : 'A Team'
}; 

function myGroup(me) { 		// 2
	me.partOf = 'A Group';  // 3
} 

myGroup(me);
console.log(me);			// 4  : {'partOf' : 'A Group'}
	
```

In the case of `myGroup` invocation, we are passing the object `me`. But unlike the example 1 scenario, we are not assigning this `me` variable to any new object, effectively meaning the object reference value within the `myGroup` function scope still is the original object's reference value and when we are modifying the property within this scope, it is effectively modifying the original object's property. Hence, you get the output from #`4`.

So does this later case not prove that javascript is pass-by-reference? No, it does not. Remember, *JavaScript passes the reference as value, in case of objects*. The confusion arises as we tend not to understand fully what pass by reference is. This is the exact reason, some prefer to call this as *call-by-sharing*.


*Initially posted by the author on [js-by-examples](https://github.com/bmkmanoj/js-by-examples/blob/master/examples/js_pass_by_value_or_reference.md)*
