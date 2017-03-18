---
layout: post

title: 在 AngularJs 防止不必要的 scope 建立
tip-number: 62
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: 在這個 tip 我會示範如何在 scope 之件傳送資料，防止 `ng-repeat` 和 `ng-if` 建立不必要的 scope
tip-writer-support: https://www.coinbase.com/loverajoel

categories:
    - zh_TW
    - angular
---

AngularJs 最受歡迎的特性之一是理解和防止 ```ng-model``` 資料的 scope，這會是你經常遇到的主要挑戰之一。
在處理 ```ng-model``` 資料時，新的不必要的 scope 透過 ```ng-repeat``` 或 ```ng-if``` 程序被建立。
看看下面的例子：


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

在上面的範例中，```innerScope``` 繼承了 ```outerScope``` 並傳送值到 ```outerScope```。
如果你輸入一個值到 ```innerScope``` 它將反映在 ```outerScope```。但是如果你編輯 ```outerScope```，
```innerScope``` 並不會反映與 ```outerScope``` 相同的值，因為 ```innerScope``` 建立了它本身的作用域，所以不再繼承自 ```outerScope```。

為了防止發生這件事，我們可以使用「Controller As」方式而不是使用 scope 作為一個 container 給所有資料和 function。但是一個更吸引人的解決方法是保持所有事物在 object，如下面範例：


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

現在 ```innerScope``` 不再建立一個新的作用域，在 ```innerScope``` 或 ```outerScope``` 編輯數值將會反映到 ```innerScope``` 和 ```outerScope```。
