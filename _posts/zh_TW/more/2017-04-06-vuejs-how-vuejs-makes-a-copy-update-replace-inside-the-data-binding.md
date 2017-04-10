---
layout: post

title: Vuejs 如何在資料綁定時，拷貝、更新並取代原來的資料
tip-number: 71
tip-username: pansila
tip-username-profile: https://github.com/pansil
tip-tldr: 在這篇 Tip，我將介紹一個範例來示範 Vuejs 可能和其他框架產生的衝突。

categories:
    - zh_TW
    - more
---

### 概觀

Vuejs 是一個相當優雅的軟體，相對於其他流行的框架像是 Angularjs 和 Reactjs，它讓你保持簡潔而且強大。
你以前可能因為害怕而放棄那些複雜的框架，但是 Vuejs 不像上面那些框架這麼複雜，你可以很快速的上手。

如果你不知道它是如何運作的，你可能會時常在踩地雷。這裡是另一個簡單而且受歡迎的 Framework7 UI 框架衝突的範例。

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

你可能會很驚訝它不能正常的運作，在新的頁面載入後沒有任何的改變。事實上，Vue 內部拷貝了目標 HTML template 元素，在透過綁定後，新的拷貝資料會取代原先的舊資料。當頁面載入時，Framework7 調用 `PageInit` callback，接著 Vue 在 `<page>` 元素進行更新。現在 DOM Tree 有了新的 `<page>` 拷貝元素，而 Framework7 在不知情的情況下持續執行剩餘的初始化工作在舊的 `<page>` 元素，最後顯示出來這就是根本的原因。

為了要解決它，別讓 Vue selector 目標在 `<page>` 元素，而是在它的子元素。這樣 Vuejs 在做資料綁定時不會影響整個頁面了。

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
- [Framework7](https://framework7.io/)
