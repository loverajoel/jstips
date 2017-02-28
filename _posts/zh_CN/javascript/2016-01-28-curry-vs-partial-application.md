---
layout: post

title: 柯里化(currying)与部分应用(partial application)
tip-number: 28
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: 柯里化(currying)与部分应用(partial application)是两种将一个函数转换为另一个有着较小普通参数个数的函数的方法。

redirect_from:
  - /zh_cn/curry-vs-partial-application/

categories:
    - zh_CN
    - javascript
---

**柯里化(currying)**

柯里化是使一个函数

f: X * Y -> R

转变为

f': X -> (Y -> R)

与用两个参数调用f不同，我们用一个参数运行f'。返回的结果是一个函数，然后用第二个参数调用此函数，得到结果。

如此，如果未柯里化的函数f这样调用

f(3,5)

柯里化后的函数f'是这样调用的

f(3)(5)

比如:
未柯里化的函数add()

```javascript

function add(x, y) {
  return x + y;
}

add(3, 5);   // returns 8
```

柯里化后的add()

```javascript
function addC(x) {
  return function (y) {
    return x + y;
  }
}

addC(3)(5);   // returns 8
```

**柯里化的规则** 

柯里化将一个二元函数，转变为一元函数，这个函数将返回另一个一元函数。

curry: (X × Y → R) → (X → (Y → R))

Javascript Code:

```javascript
function curry(f) {
  return function(x) {
    return function(y) {
      return f(x, y);
    }
  }
}
```

**部分应用(partial application)**

部分应用将一个函数

f: X * Y -> R

的第一个参数固定而产生一个新的函数

f`: Y -> R

f'与f不同，只需要填写第二个参数，这也是f'比f少一个参数的原因。

比如：将函数add的第一个参数绑定为5来产生函数plus5。

```javascript
function plus5(y) {
  return 5 + y;
}

plus5(3);  // returns 8
```

**部分应用的规则** 

部分应用使用一个二元函数和一个值产生了一个一元函数。

partApply : ((X × Y → R) × X) → (Y → R)

Javascript Code:

```javascript
function partApply(f, x) {
  return function(y) {
    return f(x, y);
  }
}
```
