---
layout: post

title: 在子元件 Keys 是很重要的
tip-number: 02
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: 從陣列中動態建立所有元件時，你必須傳送 key 屬性。它是一個唯一以及固定的 id，React 用來識別 DOM 裡面的每個元件，並區別它是否為同一個元件。使用 keys 可以確保子元件不會被重覆建立，也可以防止奇怪的事件發生。

categories:
    - zh_TW
---

從陣列中動態建立所有元件時，你必須傳送 [key](https://facebook.github.io/react/docs/multiple-components.html#dynamic-children) 屬性。它是一個唯一以及固定的 id，React 用來識別 DOM 裡面的每個元件，並區別它是否為同一個元件。使用 keys 可以確保子元件不會被重覆建立，也可以防止奇怪的事件發生。

> Key 跟效能不太相關，它跟元件識別有關係（反之，它間接提升了效能）。隨機賦值和改變數值將無法識別。[Paul O’Shannessy](https://github.com/facebook/react/issues/1342#issuecomment-39230939)

- 使用物件內存在的唯一值。
- 在你的父元件定義 keys，而不是子元件。

```javascript
//bad
...
render() {
	<div key={{item.key}}>{{item.name}}</div>
}
...

//good
<MyComponent key={{item.key}}/>
```
- [使用陣列索引是不好的習慣。](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318#.76co046o9)
- `random()` 將無法使用。

```javascript
//bad
<MyComponent key={{Math.random()}}/>
```


- 你可以建立你自己唯一的 id。確認這個方法夠快速可以附加到你的物件上。
- 當你的子元件數量很多或者含有龐大的元件，使用 keys 可以提高效能。
- [你必須提供 key 屬性給 ReactCSSTransitionGroup 的所有子元件。](http://docs.reactjs-china.com/react/docs/animation.html)
