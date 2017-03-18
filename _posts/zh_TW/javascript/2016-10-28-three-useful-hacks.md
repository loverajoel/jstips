---
layout: post

title: 三個有用的技巧
tip-number: 60
tip-username: leandrosimoes
tip-username-profile: https://github.com/leandrosimoes
tip-tldr: 三個非常有用的技巧來加速你的開發速度。


redirect_from:
  - /zh_tw/three-useful-hacks/

categories:
    - zh_TW
    - javascript
---

#### 由後往前取得陣列數值：

如果你想要由後往前取得陣列的數值，可以這麼做：

```javascript
var newArray = [1, 2, 3, 4];

console.log(newArray.slice(-1)); // [4]
console.log(newArray.slice(-2)); // [3, 4]
console.log(newArray.slice(-3)); // [2, 3, 4]
console.log(newArray.slice(-4)); // [1, 2, 3, 4]
```

#### Short-circuits 狀態

如果你有一個 function，它的狀態為 `true`，像是這樣：

```javascript
if (condition){
    dosomething();
}
```

你可以像這樣使用 short-circuit：

```javascript
condition && dosomething();
```


#### 使用「||」設定變數的預設值


如果你要在變數設定一個預設值，你可以這麼做：

```javascript
var a;

console.log(a); //undefined

a = a || 'default value';

console.log(a); //default value

a = a || 'new value';

console.log(a); //default value
```
