---
layout: post

title: Vuejs在資料綁定時會複製更新並替換目標元素
tip-number: 71
tip-username: pansila
tip-username-profile: https://github.com/pansila
tip-tldr: 在這個提示中，我會通過一個例子向您展示Vue會如何與其它軟體衝突如果你不知道這一點。

categories:
    - zh_CN
---

### 概述

Vuejs是一款簡單而強大的軟體傑作，類似其它流行的UI框架，Angularjs和Reactjs，但不像這兩者令人生畏的複雜性，Vue非常簡單，在從入門到放棄之前，你能很快掌握它的全部知識並投入生產。

但是如果你不知道它怎麼工作的，有時候它也會難為你。這裡是一個和其它UI框架(Framework7)衝突的例子。

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

你可能會驚訝它竟然無法工作，新的page點擊後並沒有顯示出來。事實上，Vue內部會複製目標HTML元素，然後根據綁定的資料更新並替換原來的元素。當Framework7載入新的頁面時，它會調用`PageInit`回呼函數，這裡我們又調用了Vue在`<page>`元素上資料綁定，這之後DOM樹裡面包含的已經是新的`<page>`元素，但Framework7對此並不知情又接著在舊的`<page>`元素上完成剩下的初始化工作，比如最終顯示這個新的頁面，這就是根本原因。

為了繞過這個問題，不要讓Vue的元素選擇器錨定在`<page>`元素上，而是定在它的子元素，這樣Vue做資料綁定時就不會影響到整個頁面顯示。

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

### 更多資訊

- [Vue](https://github.com/Vuejs/Vue)
- [Vue教程] (https://cn.vuejs.org/)
- [Framework7](https://framework7.io/)