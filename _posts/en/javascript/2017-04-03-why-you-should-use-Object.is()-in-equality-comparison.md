---
layout: post

title: Why you should use Object.is() in equality comparison 
tip-number: 68
tip-username: TarekAlQaddy
tip-username-profile: https://github.com/TarekAlQaddy
tip-tldr: A good solution for the looseness of equality comparisons in javascript 

categories:
    - en
    - javascript
---

We all know that JavaScript is loosely typed and in some cases it fall behind specially when it comes to quality comparison with '==', comparing with '==' gives unexpected results due to whats called coercion or casting "converting one of the 2 operands to the other's type then compare".

``` javascript
0 == ' ' //true
null == undefined //true
[1] == true //true
```

So they provided us with the triple equal operator '===' which is more strict and does not coerce operands, However comparing with '===' is not the best solution you can get:

``` javascript
NaN === NaN //false
```

The great news that in ES6 there is the new 'Object.is()' which is better and more precise it has the same features as '===' and moreover it behaves well in some special cases:

``` javascript
Object.is(0 , ' '); //false
Object.is(null, undefined); //false
Object.is([1], true); //false
Object.is(NaN, NaN); //true
```

Mozilla team doesn't think that Object.is is "stricter" than '===', they say that we should think of how this method deal with NaN, -0 and +0 but overall I think it is now a good practice in real applications.

Now this table illustrates..

![differences of operators in equality comparisons javascript](http://i.imgur.com/pCyqkLc.png)

## References:
[Equality comparisons and sameness](http://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)

