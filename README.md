![header](https://raw.githubusercontent.com/loverajoel/jstips/master/resources/jstips-header-blog.gif)

# Introducing JavaScript Tips
> New year new project, this is about **one JS tip every day!**

With great excitement, I introduce Javscript tips, the idea is a short and advance tip every day, that allow us improve our way of write code. The tips will be readble in less than 3 minutes and will be about performance, native js, frameworks, conventinos, hacks, interview questions and what the future of the awesome lenguage nos depare.

Every day, weekends and non laboral day incluisve, at the middle of the day I will send a tip to Github and I will tweet it.

In order to start, a gift. This is an example of how the tips would be.

## Insert item inside an array
> 12/19/2015

Insert an item into an existing array is a daily common task. You can add elements to the end of an array using push, to the beginning using unshift, or the middle using splice.
But those known methods doesn't mean that are the more porformant, here we go...

Add a element at the end of the array is easy with push(), but there are a way more performant.

```javascript
var arr = [1,2,3,4,5];

arr.push(6);
arr[arr.length] = 6; // 43% faster in Chrome 46
```
Both methods modify the original array. Doesn't belive me? Check the [jsperf](http://jsperf.com/push-item-inside-an-array)

Now we are trying to add a item to the beginning of the array 

```javascript
var arr = [1,2,3,4,5];

arr.unshift(0);
[0].concat(arr); // 98% faster in Chrome 46
```
Here a litle bit detail, unshift edit the original array, concat return a new array. [jsperf](http://jsperf.com/unshift-item-inside-an-array)

Add items at the middle of an array is easy con splice and is the most performant way to do it.

```javascript
var items = ['one', 'two', 'three', 'four'];
items.splice(2, 0, 'hello');
```

### Can you colaborate?
Sure, send a PR with the tip and we can review and publish it.
If you have improvments or sugestions about the tips, PR are welcome!
[Here the instructions](https://github.com/loverajoel/jstips/blob/master/CONTRIBUTING.md)

### Stay in touch
For updates star and watch the repo and follow the [Twitter account](https://twitter.com/tips_js) ***I will send only one tweet per day, I promise!***

### License
[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png)](http://creativecommons.org/publicdomain/zero/1.0/)