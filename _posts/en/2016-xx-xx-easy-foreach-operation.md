---
layout: post

title: Easy forEach operation
tip-number: xx
tip-username: sekaiamber
tip-username-profile: https://github.com/sekaiamber
tip-tldr: Make an easy `forEach` operation by using a simple regular expression.

categories:
    - en
---

We can use a simple regular expression `/[^, ]+/g` to make an easy `forEach` operation.  
For example, in jQuery, we can find a lot of DOM manipulations in pairs, like `append` and `appendTo`, they are just exchange the matched elements and target elements. So, we can code like this:
```javascript
jQuery = {
    // ...
    append: function(target) {
        // ...
    },
    prepend: function(target) {
        // ...
    }
    // ...
}

"append,prepend".replace(/[^, ]+/g, function (name) {
    jQuery[name + "To"] = function (selector) {
        jQuery(selector)[name](this);
        // ...
    }
});
```

**Note:** jQuery use its own `each` function to do this, see [source](https://github.com/jquery/jquery/blob/master/src/manipulation.js#L450).  

Another example, usually we don't want to expose all function of an object to users, we can simply do like this:
```javascript
// suppose myQuery is my own javascirpt framework
(function($) {
    var _allApi = {
        func1 : function() { ... },
        func2 : function() { ... },
        func3 : function() { ... },
    }
    "fun1,fun3".replace(/[^, ]+/g, function (name) {
        $[name] = _allApi[name];
    });
    return $;
})(myQuery)

myQuery.fun1(); // OK.
myQuery.fun2(); // undefined is not a function.
myQuery.fun3(); // OK.
```
