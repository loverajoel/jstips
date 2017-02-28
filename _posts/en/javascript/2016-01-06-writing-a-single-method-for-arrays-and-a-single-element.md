---
layout: post

title: Writing a single method for arrays and a single element
tip-number: 06
tip-username: mattfxyz
tip-username-profile: https://twitter.com/mattfxyz
tip-tldr: Rather than writing separate methods to handle an array and a single element parameter, write your functions so they can handle both. This is similar to how some of jQuery's functions work (`css` will modify everything matched by the selector).

redirect_from:
  - /en/writing-a-single-method-for-arrays-and-a-single-element/

categories:
    - en
    - javascript
---

Rather than writing separate methods to handle an array and a single element parameter, write your functions so they can handle both. This is similar to how some of jQuery's functions work (`css` will modify everything matched by the selector).

You just have to concat everything into an array first. `Array.concat` will accept an array or a single element.

```javascript
function printUpperCase(words) {
  var elements = [].concat(words || []);
  for (var i = 0; i < elements.length; i++) {
    console.log(elements[i].toUpperCase());
  }
}
```

`printUpperCase` is now ready to accept a single node or an array of nodes as its parameter.  It also avoids the potential `TypeError` that would be thrown if no parameter was passed.

```javascript
printUpperCase("cactus");
// => CACTUS
printUpperCase(["cactus", "bear", "potato"]);
// => CACTUS
//  BEAR
//  POTATO
```
