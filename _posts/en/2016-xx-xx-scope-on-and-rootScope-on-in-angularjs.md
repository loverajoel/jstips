---
layout: post

title: $scope.on() and $rootScope.on() in angularjs
tip-number: xx
tip-username: xiaoyu5256
tip-username-profile: https://github.com/xiaoyu5256
tip-tldr: If we use $state.reload() by angular-ui's UI-Router,we will find that,$rootScope.on() will trigger many times;That's because when we call $state.reload(),$scope.on() will unbind,but $rootScope.on() will not. we can resolve it by two way.

categories:
    - en
---

If we use ```$state.reload()``` by angular-ui's UI-Router,we will find that,```$rootScope.on()``` will trigger many times;That's because when we call ```$state.reload()```,```$scope.on()``` will unbind,but ```$rootScope.on()``` will not. we can resolve it by two way.

```javascript
// one way: unbind when scope destroy

var listener = $rootScope.on('event',function(){
  console.log("trigger event");
})
$scope.on('$destroy',listener);

// another way: check listener is exist
//define listener outside
var listener;
!listener && listener = $rootScope.on('event',function(){
  console.log("trigger event");
});

```
