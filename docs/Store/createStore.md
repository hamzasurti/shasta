# createStore()

A store holds the entire state tree of your application.

The only way to change the state inside it is to dispatch an action on it, which triggers a reducer to modify the state in an immutable way.

To create it, pass a root reducer and some other options to it:

```js
const store = createStore({
  reducers: [
    reducerFunction
  ],
  initialState: Map({
    someStuff: 'yep'
  })
})
```

## Options

- `initialState`
  - Optional (defaults to `Map()`)
  - Expects an Immutable.js type
    - You probably want to use a `Map()` here
  - This is the initial state of your store passed to your reducers
- `reducers`
  - Optional (defaults to `[]`)
  - Expects an array of reducer functions or reducer objects
  - This array is passed directly to [`combineReducers`](../combineReducers.md) to create the final reducer function
- `middleware`
  - Optional (defaults to `[]`)
  - Expects an array of middleware functions
    - Middleware functions intercept actions before they reach the store
- `enhancers`
  - Optional (defaults to `[]`)
  - Expects an array of store enhancer functions
    - Store enhancers allow you to plug in third-party capabilities like time travel, persistence, etc.
- `hooks`
  - Optional (defaults to `[]`)
  - Expects an array of hook functions
    - Hooks are called after the store has being created
    - Hooks receive one argument, the store instance
- `plugins`
  - Optional (defaults to `[]`)
  - Expects an array of plugin objects
    - [Plugins](../Plugins.md) can export any combination of middleware, reducers, hooks, and enhancers
    - This removes a ridiculous amount of boilerplate where you have to individually wire up every piece of a module you want to use

## Example

```js
import { createStore, createReducer } from 'shasta'
import { List, Map } from 'immutable'
import * as router from 'shasta-router'

const reducer = createReducer({
  counter: {
    initialState: Map({ count: 0 }),
    increment: (state) => state.update('count', v => ++v),
    decrement: (state) => state.update('count', v => --v),
  },
  people: {
    initialState: List(),
    add: (state, user) => state.push(user)
  }
})

const store = createStore({
  reducers: [
    reducer
  ],
  plugins: [
    router
  ]
})
```

## Considerations

Coming soon
