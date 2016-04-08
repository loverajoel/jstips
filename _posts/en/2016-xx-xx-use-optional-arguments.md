---
layout: post

title: How to use optional arguments in functions (with optional callback)
tip-number: xx
tip-username: alphashuro
tip-username-profile: https://github.com/alphashuro
tip-tldr: You can make function arguments and callback optional

categories:
    - en
---

Example function where arguments 2 and 3 are optional
```js
    function example( err, optionalA, optionalB, callback ) {
        // retrieve arguments as array
        var args = [].slice.call(arguments);
        
        // first argument is the error object
        // shift() removes the first item from the
        // array and returns it
        err = args.shift();

        // if last argument is a function then its the callback function.
        // pop() removes the last item in the array
        // and returns it
        if (typeof args[args.length-1] === 'function') { 
            callback = args.pop();
        }
        
        // if args still holds items, these are
        // your optional items which you could
        // retrieve one by one like this:
        if (args.length > 0) optionalA = args.shift(); else optionalA = null;
        if (args.length > 0) optionalB = args.shift(); else optionalB = null;

        // continue as usual: check for errors
        if (err) { 
            return callback && callback(err);
        }
        
        // for tutorial purposes, log the optional parameters
        console.log('optionalA:', optionalA);
        console.log('optionalB:', optionalB);
        console.log('callback:', callback);

        /* do your thing */

    }


    // invoke example function with and without optional arguments
    
    example(null, 'AA');

    example(null, function (err) {   /* do something */    });

    example(null, 'AA', function (err) {});

    example(null, 'AAAA', 'BBBB', function (err) {});
```

### How do you determine if optionalA or optionalB is intended?

Design your function to require optionalA in order to accept optionalB
