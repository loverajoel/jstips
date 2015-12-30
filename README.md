![header](https://raw.githubusercontent.com/loverajoel/jstips/master/resources/jstips-header-blog.gif)

# Introducing Javascript Tips
> New year, new project. **A JS tip per day!**

With great excitement, I introduce short and useful Javascript tips per day that will allow you to improve your code writing. With less than 2 minutes each day, you will be able to read about performances, frameworks, conventions, hacks, interview questions and all the items that the future of this awesome language holds for us.

At midday, no matter if it is a weekend or a holiday, a tip will be posted and tweeted.

Just to give you a glance, this is an example of how the tips would be like.

## Insert a new item into an array
> 12/29/2015

Inserting a new item into an existing array is a common daily task. You may append elements to the array using [`Array.prototype.push()`](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/push), prepend them using [`Array.prototype.unshift()`](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift), or insert them inbetween using [`Array.prototype.splice()`](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/splice).
But although these are the best known methods for those tasks, better performing ways do exist.

Adding an element at the end of the array is easy with [`Array.prototype.push()`](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/push) but there's a faster alternative:
```javascript
var arr = [1,2,3,4,5];

arr.push(6);
arr[arr.length] = 6; // 43% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
Don't believe me? Check the [jsperf](http://jsperf.com/push-item-inside-an-array)!
Both methods will modify the original array. 

Lets prepend an item to the the array:
```javascript
var arr = [1,2,3,4,5];

arr.unshift(0);
[0].concat(arr); // 98% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
Instead of using unshift we can also create a fresh array and join it with `arr`. [`Array.prototype.concat()`](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/push) will combine both into a new array and return the result. 
Check the [jsperf](http://jsperf.com/unshift-item-inside-an-array)!

For inserting elements inbetween the existing ones [`Array.prototype.splice()`](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/splice) turns out to be the best option.
```javascript
var items = ['one', 'two', 'three', 'four'];
items.splice(2, 0, 'hello');
```
I tried run these test in various navigators and os and the results were similar. 
Please do perform your own tests. I hope these tips turn out to be useful!

### Can you help us enrich it?
Please feel free to send us a PR with your own Javascript tip to be published here.
Any improvements or suggestions are more than welcome!
[Click to see the instructions](https://github.com/loverajoel/jstips/blob/master/CONTRIBUTING.md)

### Let’s keep in touch
To get updates, watch the repo and follow [@tips_js](https://twitter.com/tips_js), only one tweet will be sent per day. That's a deal!
> Don't forget to star the repo, this will help to spread the project!

# Tips list
> Return back the January 1st

### License
[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png)](http://creativecommons.org/publicdomain/zero/1.0/)
