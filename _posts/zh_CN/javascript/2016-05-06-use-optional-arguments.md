---
layout: post

title: 函数中如何使用可选参数（包括可选回调函数）
tip-number: 54
tip-username: alphashuro
tip-username-profile: https://github.com/alphashuro
tip-tldr: 使函数的参数与回调函数为可选参数。

redirect_from:
  - /zh_cn/use-optional-arguments/

categories:
    - zh_CN
    - javascript
---

实例函数中第2个与第3个参数为可选参数

```javascript
    function example( err, optionalA, optionalB, callback ) {
        // 使用数组取出arguments
        var args = new Array(arguments.length);
        for(var i = 0; i < args.length; ++i) {
            args[i] = arguments[i];
        };
        
        // 第一个参数为错误参数
        // shift() 移除数组中第一个参数并将其返回
        err = args.shift();

        // 如果最后一个参数是函数，则它为回调函数
        // pop() 移除数组中最后一个参数并将其返回
        if (typeof args[args.length-1] === 'function') { 
            callback = args.pop();
        }
        
        // 如果args中仍有元素，那就是你需要的可选参数
        // 你可以像这样一个一个的将其取出：
        if (args.length > 0) optionalA = args.shift(); else optionalA = null;
        if (args.length > 0) optionalB = args.shift(); else optionalB = null;

        // 像正常一样继续：检查是否有错误
        if (err) { 
            return callback && callback(err);
        }
        
        // 为了教程目的，打印可选参数
        console.log('optionalA:', optionalA);
        console.log('optionalB:', optionalB);
        console.log('callback:', callback);

        /* 你想做的逻辑 */

    }

    // ES6语法书写更简短
    function example(...args) {
        // 第一个参数为错误参数
        const err = args.shift();
        // 如果最后一个参数是函数，则它为回调函数
        const callback = (typeof args[args.length-1] === 'function') ? args.pop() : null;

        // 如果args中仍有元素，那就是你需要的可选参数你可以像这样一个一个的将其取出：
        const optionalA = (args.length > 0) ? args.shift() : null;
        const optionalB = (args.length > 0) ? args.shift() : null;
        // ... 重复取更多参数

        if (err && callback) return callback(err);

        /* 你想做的逻辑 */
    }

    // 使用或不适用可选参数调用实例函数
    
    example(null, 'AA');

    example(null, function (err) {   /* do something */    });

    example(null, 'AA', function (err) {});

    example(null, 'AAAA', 'BBBB', function (err) {});
```

### 如何保证optionalA和optionalB是预期的值?

设计你的函数，使其在接收optionalB时optionalA为必选参数。
