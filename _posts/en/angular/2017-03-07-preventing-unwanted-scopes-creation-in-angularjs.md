---
layout: post

title: Preventing Unwanted Scopes Creation in AngularJs
tip-number: 62
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: In this tip I am going to show how to pass data between scopes preventing unwanted scopes created by `ng-repeat` and `ng-if`
tip-writer-support: https://www.coinbase.com/loverajoel

categories:
    - en
    - angular
---

One of the most appreciated features of AngularJs is thUnderstanding and preventing ```ng-model``` data scope is one of the main challenge you get quite often.
While working with ```ng-model``` data, new unwanted scope can be created by  ```ng-repeat``` or ```ng-if``` procedures.
Take a look on following example-


```js
<div ng-app>
  <input type="text" ng-model="data">
   <div ng-repeat="i in [1]">
       <input type="text" ng-model="data"><br/>
        innerScope:{{data}}
   </div>
   outerScope:{{data}}
</div>
```

In the above example, ```innerScope``` inherits from ```outerScope``` and pass the value in ```outerScope```.
If you input a value in ```innerScope``` it will reflect in ```outerScope```. But if you edit ```outerScope```,
```innerScope``` doesn’t reflect the same value as ```outerScope``` because ```innerScope``` creates its own field
so no longer inherits from ```outerScope```.

To prevent this to happen we can use “Controller As” approach instead of using scope as a container
for all data and functions. But one more catchy solution is to keep everything in objects as shown is below example- 


```js
<div ng-app>
  <input type="text" ng-model="data.text">
   <div ng-repeat="i in [1]">
       <input type="text" ng-model="data.text"><br/>
        inner scope:{{data.text}}
   </div>
   outer scope:{{data.text}}
</div>
```

Now ```innerScope``` is no longer creates a new field and editing value in either ```innerScope``` or ```outerScope``` will
reflect in both ```innerScope``` and ```outerScope```.
