---
layout: post

title: State to Props maps with memory
tip-number: 66
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: You've been building your React apps with a Redux store for quite a while, yet you feel awkward when your components update so often. You've crafted your state thoroughly, and your architecture is such that each component gets just what it needs from it, no more no less. Yet, they update behind your back. Always mapping, always calculating.
tip-writer-support: https://www.coinbase.com/loverajoel

categories:
    - en
    - react
---

You've been building your React apps with a Redux store for quite a while,
yet you feel awkward when your components update so often. You've crafted
your state thoroughly, and your architecture is such that each component
gets just what it needs from it, no more no less. Yet, they update behind
your back. Always mapping, always calculating.

## Reselector to the rescue

How could would it be if you could just calculate what you need? If this
part of the state tree changes, then yes, please, update this.

Let's take a look at the code for a simple TODOs list with a visibility filter,
specially the part in charge of getting the visible TODOs in our container
component:


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

Each time our component is updated, this needs be recalculated again. Reselector
actually allows us to give our `getVisibleTodos` function memory. So it knows
whether the parts of the state we need have changed. If they have, it will
proceed, if they haven't, it will just return the last result.


Let's bring selectors!

```javascript
const getVisibilityFilter = (state) => state.visibilityFilter
const getTodos = (state) => state.todos
```

Now that we can *select* which parts of the state we want to keep track of,
we're ready to give memory to getVisibleTodos

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

And change our map to give the full state to it:

```javascript
const mapStateToProps = (state) => {
  return {
    todos: getVisibleTodos(state)
  }
}
```

And that's it! We've given memory to our function. No extra calculations if
the involved parts of the state haven't changed!