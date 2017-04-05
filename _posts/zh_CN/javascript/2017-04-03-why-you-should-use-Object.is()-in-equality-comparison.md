---
layout: post

title: 为什么你应该在相等比较中使用 Object.is()  
tip-number: 68
tip-username: TarekAlQaddy
tip-username-profile: https://github.com/TarekAlQaddy
tip-tldr: JavaScript 中一个很棒的相等比较解决方案

categories:
    - zh_CN
    - javascript
---

我们都知道 JavasSript 是弱类型的，并且当我们使用 '==' 作比较时，在一些情况下由于类型转换或者说“把两个操作数中的一个转换成另一个，然后在比较”，会出现意想不到的结果。

``` javascript
0 == ' ' //true
null == undefined //true
[1] == true //true
```

因此 JavaScript 中给我们提供了全等操作符 '===', 它比不全等操作符更加严格并且不会发生类型转换。但是用 '===' 来进行比较并不是最好的解决方案。你可能会得到：

``` javascript
NaN === NaN //false
```

好消息是 ES6 中提供了新的 'Object.is()' 方法，它具有 '===' 的一些特点，而且更好、更精确，在一些特殊案例中表现的很好：

``` javascript
Object.is(0 , ' '); //false
Object.is(null, undefined); //false
Object.is([1], true); //false
Object.is(NaN, NaN); //true
```

Mozilla 团队并不认为 Object.is 比 '===' 更加‘严格’，他们说我们应该考虑的是这个方法如何处理 NaN, -0 和 +0。但是总的来说， 我认为它在实际应用中是一个很好的实践。

现在来看看这张图表的对比...

![differences of operators in equality comparisons javascript](http://i.imgur.com/pCyqkLc.png)

## References:
[Equality comparisons and sameness](http://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)

