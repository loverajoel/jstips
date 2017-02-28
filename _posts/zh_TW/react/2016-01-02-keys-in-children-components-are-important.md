---
layout: post

title: 在子元件 Keys 是很重要的
tip-number: 02
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: 你可以從陣列動態建立 key 屬性並傳送到所有的元件（component）。它是一個唯一以及固定的 id，React 用來識別 DOM 裡面的每個元件，並區別它是否為同一個元件。使用 keys 可以確保子元件被保護而不會被重覆建立，也可以防止奇怪的事件發生。
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /zh_tw/keys-in-children-components-are-important/

categories:
    - zh_TW
    - react
---

你可以從陣列動態建立 [key](https://facebook.github.io/react/docs/multiple-components.html#dynamic-children) 屬性並傳送到所有的元件（component）。它是一個唯一以及固定的 id，React 用來識別 DOM 裡面的每個元件，並區別它是否為同一個元件。使用 keys 可以確保子元件被保護而不會被重覆建立，也可以防止奇怪的事件發生。

> Key 跟效能不太相關，它跟元件識別較有關係（反之，它間接提升了效能）。隨機賦值和改變數值將無法識別。[Paul O’Shannessy](https://github.com/facebook/react/issues/1342#issuecomment-39230939)

- 使用物件內存在的唯一值。
- 在你的父元件定義 keys，而不是子元件。

```javascript
//bad
...
render() {
	<div key={% raw %}{{item.key}}{% endraw %}>{% raw %}{{item.name}}{% endraw %}</div>
}
...

//good
<MyComponent key={% raw %}{{item.key}}{% endraw %}/>
```
- [使用陣列索引是不好的習慣。](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318#.76co046o9)
- `random()` 將無法使用。

```javascript
//bad
<MyComponent key={% raw %}{{Math.random()}}{% endraw %}/>
```


- 你可以建立你自己唯一的 id。確認這個方法夠快速可以附加到你的物件上。
- 當你的子元件數量很多或者含有龐大的元件，使用 keys 可以提高效能。
- [你必須提供 key 屬性給 ReactCSSTransitionGroup 的所有子元件。](http://docs.reactjs-china.com/react/docs/animation.html)
