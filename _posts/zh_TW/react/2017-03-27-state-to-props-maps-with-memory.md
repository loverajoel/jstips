---
layout: post

title: 從 State 到 Prop 的映射
tip-number: 66
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: 你可能在你建立的 React Apps 使用 Redux Store 有段時間了，當 component 經常更新時，你可能會感到很不便。 你已經徹底建立你的 state，而且架構你的每個 component 所需要的 state。然而在這些更新 state 的背後，總是在做 state 的 map 和計算。
tip-writer-support: https://www.coinbase.com/loverajoel

categories:
    - zh_TW
    - react
---

你可能在你建立的 React Apps 使用 Redux Store 有段時間了，當 component 經常更新時，你可能會感到很不便。 你已經徹底建立你的 state，而且架構你的每個 component 所需要的 state。然而在這些更新 state 的背後，總是在做 state 的 map 和計算。

## 使用 Reselector 來拯救

如何只計算我們所需要的 state？如果這個 state tree 的部分改變了，沒錯！請更新 state。

讓我看一下簡單的 TODOs List，特別是在我們的 container 負責取得 visible TODOs 的 visibility filter 程式碼：


```javascript
const getVisibleTodos = (todos, filter) => {
  switch (filter) {
    case 'SHOW_ALL':
      return todos
    case 'SHOW_COMPLETED':
      return todos.filter(t => t.completed)
    case 'SHOW_ACTIVE':
      return todos.filter(t => !t.completed)
  }
}

const mapStateToProps = (state) => {
  return {
    todos: getVisibleTodos(state.todos, state.visibilityFilter)
  }
}
```

在每次我們的 component 被更新時，它們都需要被重新計算一遍。事實上，Reselector 允許我們取得我們的 `getVisibleTodos` function 的 memory。

所以它知道我們部分的 state 是否需要改變，如果它們需要改變，它將繼續處理，如果沒有的話，它將回傳最後的結果。


讓我們使用 selectors！

```javascript
const getVisibilityFilter = (state) => state.visibilityFilter
const getTodos = (state) => state.todos
```

現在我們可以 *select* 我們想要繼續追蹤的部分 state，我們準備把 memory 給 getVisibleTodos：

```javascript
import {createSelector} from 'reselect'

const getVisibleTodos = createSelector(
  [getVisibilityFilter, getTodos],
  (visibilityFilter, todos) => {
    switch (visibilityFilter) {
      case 'SHOW_ALL':
        return todos
      case 'SHOW_COMPLETED':
        return todos.filtler(t => t.completed)
      case 'SHOW_ACTIVE':
        return todos.filter(t => !t.completed)
    }
  }
)
```

並改變我們的 map 給它完整的 state：

```javascript
const mapStateToProps = (state) => {
  return {
    todos: getVisibleTodos(state)
  }
}
```

就是這樣！我們給定 memory 到我們的 function。如果涉及的 state 沒有改變的話，不會有額外的去計算 state。
