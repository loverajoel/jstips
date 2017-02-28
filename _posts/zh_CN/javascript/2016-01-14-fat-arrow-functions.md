---
layout: post

title: 箭头函数
tip-number: 14
tip-username: pklinger
tip-username-profile: https://github.com/pklinger/
tip-tldr: 介绍一个ES6的新特性，箭头函数或许一个让你用更少行写更多代码的方便工具。

redirect_from:
  - /zh_cn/fat-arrow-functions/

categories:
    - zh_CN
    - javascript
---


介绍一个ES6的新特性，箭头函数或许一个让你用更少行写更多代码的方便工具。它的名字(fat arrow functions)来自于它的语法`=>`是一个比瘦箭头`->`要'胖的箭头'（译者注：但是国内貌似不分胖瘦就叫箭头函数）。Some programmers might already know this type of functions from different languages such as Haskell as 'lambda expressions' respectively 'anonymous functions'. It is called anonymous, as these arrow functions do not have a descriptive function name.（译者注：一些其他语言中的箭头函数，避免不准确就不翻译了 欢迎PR）

### 有什么益处呢?
* 语法: 更少的代码行; 不再需要一遍一遍的打`function`了
* 语义: 从上下文中捕获`this`关键字

### 简单的语法示例
观察一下这两个功能完全相同的代码片段。你将很快明白箭头函数做了什么。

```javascript
// 箭头函数的一般语法
param => expression

// 也可以用用小括号
// 多参数时小括号是必须的
(param1 [, param2]) => expression


// 使用functions
var arr = [5,3,2,9,1];
var arrFunc = arr.map(function(x) {
  return x * x;
});
console.log(arr)

// 使用箭头函数
var arr = [5,3,2,9,1];
var arrFunc = arr.map((x) => x*x);
console.log(arr)
```

正如你所看到的，箭头函数在这种情况下省去了写小括号，function以及return的时间。我建议你总是使用小括号，因为对于像`(x,y) => x+y`这样多参数函数，小括号总是需要的。这仅是以防在不同使用场景下忘记小括号的一种方法。但是上面的代码和`x => x*x`是一样的。至此仅是语法上的提升，减少了代码行数并提高了可读性。

### Lexically binding `this`

这是另一个使用箭头函数的好原因。这是一个关于`this`上下文的问题。使用箭头函数，你不需要再担心`.bind(this)`也不用再设置`that = this`了，因为箭头函数继承了外围作用域的`this`值。看一下下面的[示例](https://jsfiddle.net/pklinger/rw94oc11/):

```javascript

// 全局定义 this.i
this.i = 100;

var counterA = new CounterA();
var counterB = new CounterB();
var counterC = new CounterC();
var counterD = new CounterD();

// 不好的例子
function CounterA() {
  // CounterA的`this`实例 (!!调用时忽略了此实例)
  this.i = 0;
  setInterval(function () {
    // `this` 指向全局(global)对象,而不是CounterA的`this`
    // 所以从100开始计数,而不是0 (本地的this.i)
    this.i++;
    document.getElementById("counterA").innerHTML = this.i;
  }, 500);
}

// 手动绑定 that = this
function CounterB() {
  this.i = 0;
  var that = this;
  setInterval(function() {
    that.i++;
    document.getElementById("counterB").innerHTML = that.i;
  }, 500);
}

// 使用 .bind(this)
function CounterC() {
  this.i = 0;
  setInterval(function() {
    this.i++;
    document.getElementById("counterC").innerHTML = this.i;
  }.bind(this), 500);
}

// 箭头函数
function CounterD() {
  this.i = 0;
  setInterval(() => {
    this.i++;
    document.getElementById("counterD").innerHTML = this.i;
  }, 500);
}
```

更多有关箭头函数的内容可以查看[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)。更多语法选项请看[这里](http://jsrocks.org/2014/10/arrow-functions-and-their-scope/).

