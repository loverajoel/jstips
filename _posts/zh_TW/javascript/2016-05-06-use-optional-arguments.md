---
layout: post

title: 如何使用在函式中的可選參數（包含 callback）
tip-number: 54
tip-username: alphashuro
tip-username-profile: https://github.com/alphashuro
tip-tldr: 你的 function 參數和 callback 是可選參數。

redirect_from:
  - /zh-tw/use-optional-arguments/

categories:
    - javascript
    - zh-TW
---

Example function 中第二個和第三個為可選的參數：

```javascript
    function example( err, optionalA, optionalB, callback ) {
        // 以陣列形式取得參數。
        var args = new Array(arguments.length);
        for(var i = 0; i < args.length; ++i) {
            args[i] = arguments[i];
        };

        // 第一個參數是一個 error 物件，
        // 從陣列移除第一個參數，並將它回傳。
        err = args.shift();

        // 如果最後一個參數是 function，那它則為 callback function。
        // 移除在陣列中最後一個參數，並將它回傳。
        if (typeof args[args.length-1] === 'function') {
            callback = args.pop();
        }

        // 如果還有其他參數，
        // 那些都是可選參數，你可以像這樣一個一個將他取出：
        if (args.length > 0) optionalA = args.shift(); else optionalA = null;
        if (args.length > 0) optionalB = args.shift(); else optionalB = null;

        // 像往常一樣︰檢查是否有錯誤。
        if (err) {
            return callback && callback(err);
        }

        // 為了這個教學，log 是可選的參數。
        console.log('optionalA:', optionalA);
        console.log('optionalB:', optionalB);
        console.log('callback:', callback);

        /* 你任何想做的邏輯。 */

    }

    // ES6 程式碼更簡短、更簡潔。
    function example(...args) {
        // 第一個參數是一個 error 物件
        const err = args.shift();
        // 如果最後一個參數是 function，那它則為 callback function。
        const callback = (typeof args[args.length-1] === 'function') ? args.pop() : null;

        // 如果還有其他參數，那些都是可選參數，你可以像這樣一個一個將他取出：
        const optionalA = (args.length > 0) ? args.shift() : null;
        const optionalB = (args.length > 0) ? args.shift() : null;
        // ... repeat for more items

        if (err && callback) return callback(err);

        /* 你任何想做的邏輯。 */
    }

    // 調用 example function 和沒有可選的參數。

    example(null, 'AA');

    example(null, function (err) {   /* 你任何想做的邏輯。 */    });

    example(null, 'AA', function (err) {});

    example(null, 'AAAA', 'BBBB', function (err) {});
```

### 我要如何確認 optionalA 或 optionalB 是預期的？

設計你的 function，為了接受 optionalB 而要求 optionalA。