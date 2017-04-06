---
layout: post

title: VueJS, How VueJS makes a copy-update-replace inside the data binding.
tip-number: 71
tip-username: pansila 
tip-username-profile: https://github.com/pansil
tip-tldr: In this tip, I will introduce an example to show you how it might conflict with other software.

categories:
    - en
    - more
---

### Overview

Vuejs is a wonderful piece of software that keeps simple yet powerful compared to other prevalent frameworks, like Angularjs and Reactjs.
You can quickly master it before you give up by being in awe of the framework complexity unlike them above.

But it bites you sometimes if you don't know how it works. Here is an example of the conflict with another simple and popular UI framework, Framework7.

```html
<!-- index.html -->
<div class="pages">
  <div class="page" date-page="index">
    <!-- load a new page -->
    <a href="test.html">new page</a>
  </div>
</div>

<!-- test.html -->
<div class="pages">
  <div class="page" date-page="test" id="test">
    <div class="page-content" id="test1">
    <p>{% raw %}{{content}}{% endraw %}</p>
    </div>
  </div>
</div>
```

```js
var myApp = new Framework7();
myApp.onPageInit('test', function (page) {
  new Vue({
    el: '#test',
    data: {
      content: 'hello world'
    }
  });
});
```

You may be surprised that it doesn't work, nothing changed after new page loaded. In fact, Vue internally makes a copy of the target html template element and replaces the original one with the new copied one after the date binding to it. While during the page loading, Framework7 invokes the `PageInit` callback and then Vue kicks in and makes the update on the `<page>` element. Now the DOM tree has the new copied `<page>` element while Framework7 stays unconcerned and continues to perform the remaining initialization job on the old `<page>` element, like show it eventually, that's the root cause.

To work around it, don't let Vue selector targets on the `<page>` element, on its child instead. Then the copy-update-replace won't blow away the whole page anymore.

```js
var myApp = new Framework7();
myApp.onPageInit('test', function (page) {
  new Vue({
    el: '#test1',
    data: {
      content: 'hello world'
    }
  });
});
```

### More info

- [Vue](https://github.com/Vuejs/Vue)
- [Framework7](https://framework7.io/)