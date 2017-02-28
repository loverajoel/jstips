---
layout: post

title: JS中的短路求值
tip-number: 27
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: 短路求值是说, 只有当第一个运算数的值无法确定逻辑运算的结果时，才对第二个运算数进行求值：当AND(`&&`)的第一个运算数的值为false时，其结果必定为false；当OR(`||`)的第一个运算数为true时，最后结果必定为true。

redirect_from:
  - /zh_cn/short-circuit-evaluation-in-js/

categories:
    - zh_CN
    - javascript
---

[短路求值](https://zh.wikipedia.org/wiki/%E7%9F%AD%E8%B7%AF%E6%B1%82%E5%80%BC)是说, 只有当第一个运算数的值无法确定逻辑运算的结果时，才对第二个运算数进行求值：当AND(`&&`)的第一个运算数的值为false时，其结果必定为false；当OR(`||`)的第一个运算数为true时，最后结果必定为true。

对于下面的`test`条件和`isTrue`与`isFalse`方法

```js
var test = true;
var isTrue = function(){
  console.log('Test is true.');
};
var isFalse = function(){
  console.log('Test is false.');
};

```

使用逻辑与 - `&&`.

```js
// 普通的if语句
if(test){
  isTrue();    // Test is true
}

// 上面的语句可以使用 '&&' 写为：

( test && isTrue() );  // Test is true
```

使用逻辑或 - `||`.

```js
test = false;
if(!test){
  isFalse();    // Test is false.
}

( test || isFalse());  // Test is false.
```

逻辑或可以用来给参数设置默认值。

```js
function theSameOldFoo(name){
    name = name || 'Bar' ;
    console.log("My best friend's name is " + name);
}
theSameOldFoo();  // My best friend's name is Bar
theSameOldFoo('Bhaskar');  // My best friend's name is Bhaskar
```

逻辑与可以用来避免调用undefined参数的属性时报错
例如:-

```js
var dog = {
  bark: function(){
     console.log('Woof Woof');
   }
};

// 调用 dog.bark();
dog.bark(); // Woof Woof.

// 但是当dog未定义时，dog.bark() 将会抛出"Cannot read property 'bark' of undefined." 错误
// 防止这种情况，我们可以使用 &&.

dog&&dog.bark();   // This will only call dog.bark(), if dog is defined.

```
