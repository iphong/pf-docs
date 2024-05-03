# How to avoid performance issues when using React

Facebook has done a great job when creating React, a simple and flexible library, for building web-based user interfaces. However, like other technologies, React has problems related to performance. Below are some common React performance issues and how to avoid them.

## Unnecessary re-rendering

Re-rendering components while unnecessary is a common problem affecting React performance. This issue happens when a component re-renders while its props and states are not changed.

To avoid it, you should use `React.memo` or `shouldComponentUpdate`. `React.memo` is a higher-order component that memoizes a React function component and re-renders it only when its props are changed. On the other hand, `shouldComponentUpdate` is a lifecycle method that allows you to determine whether a React class component should update.

Below are examples using `React.memo` and `shouldComponentUpdate`.

{% tabs %}
{% tab title="React.memo" %}
```javascript
import React, { memo, useCallback, useState } from 'react'

const Counter1 = memo(props => {
  console.log('Render counter 1')

  return (
    <div>
      <h2>Counter 1:</h2>
      <h3>{props.value}</h3>
      <button onClick={props.onClick}>Add</button>
    </div>
  )
})

const Counter2 = memo(props => {
  console.log('Render counter 2')

  return (
    <div>
      <h2>Counter 2:</h2>
      <h3>{props.value}</h3>
      <button onClick={props.onClick}>Add</button>
    </div>
  )
})

export default function App() {
  // Define some internal states
  const [counter1, setCounter1] = useState(0)
  const [counter2, setCounter2] = useState(0)

  // Define some methods to update internal states.
  //
  // The `useCallback` hook should be used to memoize functions
  // that will be passed as props when rendering other components.
  // Otherwise, the use of `React.memo` will not work as expected.
  const increase1 = useCallback(() => {
    setCounter1(counter1 + 1)
  }, [counter1])

  const increase2 = useCallback(() => {
    setCounter2(counter2 + 1)
  }, [counter2])

  // Render app UI
  return (
    <div className="container">
      <div>
        <Counter1 value={counter1} onClick={increase1} />
      </div>
      <div>
        <Counter2 value={counter2} onClick={increase2} />
      </div>
    </div>
  )
}
```
{% endtab %}

{% tab title="shouldComponentUpdate" %}
```javascript
import React, { Component, useState } from 'react'

class Counter1 extends Component {
  shouldComponentUpdate(nextProps) {
    // Re-render the component only if the passed value is changed.
    if (nextProps.value !== this.props.value) {
      return true
    }

    return false
  }

  render() {
    console.log('Render counter 1')

    return (
      <div>
        <h2>Counter 1:</h2>
        <h3>{this.props.value}</h3>
        <button onClick={this.props.onClick}>Add</button>
      </div>
    )
  }
}

class Counter2 extends Component {
  shouldComponentUpdate(nextProps) {
    // Re-render the component only if the passed value is changed.
    if (nextProps.value !== this.props.value) {
      return true
    }

    return false
  }

  render() {
    console.log('Render counter 2')

    return (
      <div>
        <h2>Counter 2:</h2>
        <h3>{this.props.value}</h3>
        <button onClick={this.props.onClick}>Add</button>
      </div>
    )
  }
}

export default function App() {
  // Define some internal states
  const [counter1, setCounter1] = useState(0)
  const [counter2, setCounter2] = useState(0)

  // Define some methods to update internal states
  const increase1 = () => {
    setCounter1(counter1 + 1)
  }

  const increase2 = () => {
    setCounter2(counter2 + 1)
  }

  // Render app UI
  return (
    <div className="container">
      <div>
        <Counter1 value={counter1} onClick={increase1} />
      </div>
      <div>
        <Counter2 value={counter2} onClick={increase2} />
      </div>
    </div>
  )
}
```
{% endtab %}
{% endtabs %}

Note that you need to use the `useCallback` hook to memoize functions that will be passed to function components memoized by `React.memo`. Otherwise, the use of `React.memo` will not work as expected.

Besides re-rendering components while unnecessary, rendering invisible components might also cause a performance issue. Let's take a look at the example below.

```javascript
import React, { memo, useCallback, useState } from 'react'

const SayHello = memo(props => {
  console.log('Render say hello')

  return (
    <div style={{ display: props.visible ? 'block' : 'none' }}>
      <h2>Hello {props.name}!</h2>
      <button onClick={props.onClick}>Reset</button>
    </div>
  )
})

export default function App() {
  // Define some internal states
  const [name, setName] = useState('')
  const [open, setOpen] = useState(false)

  // Define some methods to update internal states
  const handleInput = useCallback(event => {
    setName(event.target.value)
  }, [])

  const openModal = useCallback(() => {
    setOpen(true)
  }, [])

  const resetNameAndCloseModal = useCallback(() => {
    setName('')
    setOpen(false)
  }, [])

  // Render app UI
  return (
    <>
      <form className="container" onSubmit={e => e.preventDefault()}>
        <label>Input your name:</label>
        <br />
        <input type="text" value={name} onChange={handleInput} />
        <br />
        <button onClick={openModal}>Say hello</button>
      </form>
      <SayHello visible={open} name={name} onClick={resetNameAndCloseModal} />
    </>
  )
}
```

The `SayHello` component is always rendered regardless of its visibility state. This behavior might not cause a noticeable performance issue if just a few components like the `SayHello` component are rendered. However, the performance will decrease when the number of invisible components increases.

To avoid this potential performance issue, render only components visible on the screen. Below is the revised version of the example.

```javascript
// Code above this line is unchanged.
      {open && (
        <SayHello visible={open} name={name} onClick={resetNameAndCloseModal} />
      )}
// Code below this line is unchanged.
```

## Memory leaks

Another common problem affecting React performance is memory leaks. This issue happens when a component does not clean up event listeners or timers that are no longer needed and causes the browser to run out of memory.

To avoid it, you should return a clean-up function when using the `useEffect` hook or define the `componentWillUnmount` lifecycle method to do clean-up work.

(work in progress)
