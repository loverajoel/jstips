---
layout: post

title: 使用 tap 来快速 debug
tip-number: 65
tip-username: loverajoel
tip-username-profile: https://twitter.com/loverajoel
tip-tldr: 在这里 tap 是一个小怪物。一个可以用来快速调试、链式调用、匿名函数，还可以打印任何你想打印的东西的函数。
tip-md-link: https://github.com/loverajoel/jstips/blob/master/_posts/en/javascript/2017-03-16-tapping-for-quick-debugging.md

categories:
    - zh_CN
    - javascript
---

在这里 tap 是一个小怪物。一个可以用来快速调试、链式调用、匿名函数，还可以打印任何你想打印的东西的函数。

``` javascript
function tap(x) {
    console.log(x);
    return x;
}
```

为什么我们不用 `console.log` 这个老方式了？让我来示范一个例子：

``` javascript
bank_totals_by_client(bank_info(1, banks), table)
            .filter(c => c.balance > 25000)
            .sort((c1, c2) => c1.balance <= c2.balance ? 1 : -1 )
            .map(c =>
                 console.log(`${c.id} | ${c.tax_number} (${c.name}) => ${c.balance}`));
```

现在，加入你从这个链式调用中没有得到任何返回。
在哪里除了问题呢？或许 `bank_info` 没有返回东西，我们需要监听（tap）它:

``` javascript
bank_totals_by_client(tap(bank_info(1, banks)), table)
```

基于我们特殊的实现，它可能会打印一些东西，也可能什么也不打印。
我们假设，打印出来的东西是正确的，因此， `bank_info` 没有问题。

我们需要继续调试下一个函数， filter.

``` javascript
            .filter(c => tap(c).balance > 25000)
```

我们可以得到 `c` 吗？如果可以，说明 `bank_totals_by_client` 运行正常。
可能是 filter 内的条件有问题？

``` javascript
            .filter(c => tap(c.balance > 25000))
```

啊哈！我们发现除了 `false` 没有打印其他东西，所以说明没有一个 client >25000，
这就是为什么方法什么也没返回的原因。

## (附) 更先进的 tap

``` javascript
function tap(x, fn = x => x) {
    console.log(fn(x));
    return x;
}
```

让我们来看一下一个更强大的怪物，如果我们想在监听（tap）之前*事先*做一些操作应该怎么办？比如，我们只想方位某个对象特定的参数，位于一个逻辑运算，等等。使用上面的方法，在调用的时候增加一个额外参数，这个函数在被监听（tap）的时候就会被执行。

``` javascript
tap(3, x => x + 2) === 3; // prints 5, but expression evaluates to true, why :-)?
```
