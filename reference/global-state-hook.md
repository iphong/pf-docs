---
cover: >-
  https://images.unsplash.com/photo-1590650043523-3e6a52de6acb?crop=entropy&cs=srgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHw2fHxob29rfGVufDB8fHx8MTYzNTkwODM3MQ&ixlib=rb-1.2.1&q=85
coverY: 0
---

# Global State Hook

## How to use

### createSubscription(initialState)

```javascript
import { createSubscription } from "global-state-hook"

const counterSubscription = createSubscription({ count: 0 })
```

### useSubscription(subscriber)

```javascript
import { createSubscription, useSubscription } from "global-state-hook"

const counterSubscription = createSubscription({ count: 0 })

// Your custom hook goes here so you can share it to anywhere
const useCounter = () => {
  let { state, setState } = useSubscription(counterSubscription)
  const increment = () => setState({ count: state.count + 1 })
  const decrement = () => setState({ count: state.count + 1 })
  return { count: state.count, increment, decrement }
}

function Counter() {
  let { count, increment, decrement } = useCounter()
  return (
    <div>
      <button onClick={decrement}>-</button>
      <span>{count}</span>
      <button onClick={increment}>+</button>
    </div>
  )
}
```

### useSubscription(subscriber, pick: string\[])

```javascript
import { createSubscription, useSubscription } from "global-state-hook"

const counterSubscription = createSubscription({ count: 0, foo: 10 })

function Foo() {
  // Only update when foo change
  let { state, setState } = useSubscription(counterSubscription, ["foo"])

  return (
    <div>
      <button onClick={() => setState({ foo: state.foo - 1 })}>-</button>
      <span>{state.foo}</span>
      <button onClick={() => setState({ foo: state.foo + 1 })}>+</button>
    </div>
  )
}
```

## Guide

#### Global state is not bad.

It's about how you manage it, global state will not be bad if you do it the right way. You can consider using `Context.Provider` to provide your global subscription so it can be clean up after the component unmounted. Example:

```
const TextContext = React.createContext < any > null

const useTextValue = () => {
  const textSubscription = useContext(TextContext)
  let { state, setState } = useSubscription(textSubscription)
  const onChange = (e) => setState({ value: e.target.value })
  return { value: state.value, onChange }
}

function Text() {
  let { value, onChange } = useTextValue()
  return (
    <div>
      <input value={value} onChange={onChange} />
    </div>
  )
}

function TextComponent() {
  const textSubscription = createSubscription({
    value: "The text will sync together",
  })
  return (
    <TextContext.Provider value={textSubscription}>
      <Text />
    </TextContext.Provider>
  )
}
```

#### Tip#1: Select your state property that you want to subscribe to

By default some people might recommend you to put only one state to a `subscription`, for example:

```
const textSubscription = createSubscription("Your initial state here")

let { state: text, setState: setText } = useSubscription(textSubscription)

// Change the text value:
setText("New text value")
```

But in case you have a very large Component with many state in it, so what is the proper way to handle? Just see my code below:

```
import { createSubscription, useSubscription } from "global-state-hook"

const multiStateSubscription = createSubscription({ foo: 1, bar: 2, baz: 3 })

function Foo() {
  // Only update when foo or baz change
  let { state, setState } = useSubscription(multiStateSubscription, [
    "foo",
    "baz",
  ])

  return (
    <div>
      <button onClick={() => setState({ foo: state.foo - 1 })}>-</button>
      <span>{state.foo}</span>
      <span>{state.baz}</span>
      <button onClick={() => setState({ foo: state.foo + 1 })}>+</button>
    </div>
  )
}
```

### Reducer pattern:

For those who still in love with redux, the reducer pattern will fit for you:

```
const counterSubscription = createSubscription({ count: 0 })
function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 }
    case "decrement":
      return { count: state.count - 1 }
    default:
      throw new Error()
  }
}

function Counter() {
  const { state, dispatch } = useReducerSubscription(
    counterSubscription,
    reducer,
  )
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({ type: "decrement" })}>-</button>
      <button onClick={() => dispatch({ type: "increment" })}>+</button>
    </>
  )
}
```

### Support debugging with React Developer Tools

[![React Dev Tools](https://raw.githubusercontent.com/paul-phan/global-state-hook/HEAD/example/react-dev-tools.png)](https://github.com/paul-phan/global-state-hook/blob/HEAD/example/react-dev-tools.png)

It's so easy right? :D

\
