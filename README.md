![header](https://raw.githubusercontent.com/loverajoel/jstips/master/resources/jstips-header-blog.gif)

# Introducing Javascript Tips
> New year, new project. **A JS tip per day!**

With great excitement, I introduce short and useful Javascript tips per day that will allow you to improve your code writing. With less than 2 minutes each day, you will be able to read about performances, frameworks, conventions, hacks, interview questions and all the items that the future of this awesome language holds for us.

At midday, no matter if it is a weekend or a holiday, a tip will be posted and tweeted.

Just to give you a glance, this is an example of how the tips would be like.

## Insert item inside an array
> 12/29/2015

Insert an item into an existing array is a daily common task. You can add elements to the end of an array using push, to the beginning using unshift, or the middle using splice.
But those known methods doesn't mean that are the more porformant, here we go...

Add a element at the end of the array is easy with push(), but there are a way more performant.

```javascript
var arr = [1,2,3,4,5];

arr.push(6);
arr[arr.length] = 6; // 43% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
Both methods modify the original array. Doesn't believe me? Check the [jsperf](http://jsperf.com/push-item-inside-an-array)

Now we are trying to add a item to the beginning of the array 

```javascript
var arr = [1,2,3,4,5];

arr.unshift(0);
[0].concat(arr); // 98% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
Here a little bit detail, unshift edit the original array, concat return a new array. [jsperf](http://jsperf.com/unshift-item-inside-an-array)

Add items at the middle of an array is easy with splice and is the most performant way to do it.

```javascript
var items = ['one', 'two', 'three', 'four'];
items.splice(2, 0, 'hello');
```
I tried run these test in various navigators and os and the results was similar, I hope you try your own test and that these tips will be useful!

## Prefer the Triple-Equals Operator
> 12/30/2015 by [madhur](https://github.com/madhur)

A concept that any beginning developer of JavaScript needs to know is the difference between the double and triple equals. With a double equals comparison operator JavaScript will be a lot more lenient with the outcome. 

```javascript
var x = 51;
var str = "51";
if(x == str) {
    console.log("Somewhat lol");
} else {
    alert("WRONG");
}
```

With the double equals, the if statement will return true and the first block will be executed. However if there was a triple equals in the same example.

```javascript
var x = 51;
var str = "51";
if(x === str) {
    console.log("Somewhat lol");
} else {
    alert("WRONG");
}
```

The alert would pop up instead. The reason being the triple equals will not convert the type of the values; making it more strict and therefore better in most situations.

### Can you help us enrich it?
Please feel free to send us a PR with your own Javascript tip to be published here.
Any improvements or suggestions are more than welcome!
[Click to see the instructions](https://github.com/loverajoel/jstips/blob/master/CONTRIBUTING.md)

### Let’s keep in touch
To get updates, watch the repo and follow the [Twitter account](https://twitter.com/tips_js), only one tweet will be sent per day. It is a deal!
> Don't forget Star the repo, this will help to diffuse the project!

# Tips list
> Return back the January 1st

### License
[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png)](http://creativecommons.org/publicdomain/zero/1.0/)