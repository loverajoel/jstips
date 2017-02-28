---
layout: post

title: 运用存储加速递归 Speed up recursive functions with memoization
tip-number: 29
tip-username: hingsir
tip-username-profile: https://github.com/hingsir
tip-tldr: 大家对斐波那契(Fibonacci)数列都很熟悉。我们可以再20秒内写出下面这样一个方法，它可以运行，但并不高效。它做了太多重复的运算，我们可以通过存储这些运算结果来使其加速。


redirect_from:
  - /zh_cn/speed-up-recursive-functions-with-memoization/

categories:
    - zh_CN
    - javascript
---

大家对斐波那契(Fibonacci)数列都很熟悉。我们可以再20秒内写出下面这样一个方法。

```js
var fibonacci = function(n){
    return n < 2 ? n : fibonacci(n-1) + fibonacci(n-2);
}
```

它可以运行，但并不高效。它做了太多重复的运算，我们可以通过存储这些运算结果来使其加速。

```js
var fibonacci = (function() {
  var cache = [0, 1]; // cache the value at the n index
  return function(n) {
    if (cache[n] === undefined) {
      for (var i = cache.length; i <= n; ++i) {
        cache[i] = cache[i-1] + cache[i-2];
      }
    }
    return cache[n];
  }
})()
```

我们也可以定义一个高阶函数，它接收一个方法作为参数，返回一个该方法运用存储后的新方法。

```js
var memoize = function(func){
    var cache = {};
    return function(){
        var key = Array.prototype.slice.call(arguments).toString();
        return key in cache ? cache[key] : (cache[key] = func.apply(this,arguments));
    }
}
fibonacci = memoize(fibonacci);
```

ES6版本的memoize函数如下：

```js
var memoize = function(func){
    const cache = {};
    return (...args) => {
        const key = [...args].toString();
        return key in cache ? cache[key] : (cache[key] = func(...args));
    }
}
fibonacci = memoize(fibonacci);
```

我们可以将`memoize()`用在很多其他地方

* GCD(最大公约数)

```js
var gcd = memoize(function(a,b){
    var t;
    if (a < b) t=b, b=a, a=t;
    while(b != 0) t=b, b = a%b, a=t;
    return a;
})
gcd(27,183); //=> 3
```

* 阶乘运算

```js
var factorial = memoize(function(n) {
    return (n <= 1) ? 1 : n * factorial(n-1);
})
factorial(5); //=> 120
```
