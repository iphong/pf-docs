# Avoid some common React performance issues

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

Note that you need to use the `useCallback` hook to memoize functions that will be passed to function components memoized by `React.memo`. Otherwise, the use of `React.memo` might not work as expected.

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

The `SayHello` component is always rendered regardless of its visibility state. This behavior might not cause a noticeable performance issue if just a few components like that are rendered. However, the performance will decrease when the number of invisible components increases.

To avoid this potential performance issue, render only components visible on the screen. Below is the revised version of the example.

```javascript
// Code above this line is unchanged.
      {open && (
        <SayHello visible={open} name={name} onClick={resetNameAndCloseModal} />
      )}
// Code below this line is unchanged.
```

## Memory leaks

Another common problem affecting React performance is memory leaks. This issue happens when a component does not clean up resources that are no longer needed and causes the browser to run out of memory.

To avoid it, you should return a clean-up function when using the `useEffect` hook or define the `componentWillUnmount` lifecycle method to do clean-up work.

Event listeners are the first common resource that should be cleaned up when no longer needed.

{% tabs %}
{% tab title="useEffect" %}
```javascript
import React, { useEffect } from 'react'

// Don't use inline event handlers.
/*
export default function App() {
  return <button onClick={() => alert('Button clicked')}>Click me</button>
}
*/

// Use event listeners and event delegation instead.
export default function App() {
  useEffect(() => {
    function handleClick(e) {
      if (e.target.tagName === 'BUTTON') {
        alert('Button clicked')
      }
    }

    document.addEventListener('click', handleClick)

    // Remove event listeners when unmounting the component.
    return () => document.removeEventListener('click', handleClick)
  }, [])

  return <button>Click me</button>
}
```
{% endtab %}

{% tab title="componentWillUnmount" %}
```javascript
import React, { Component } from 'react'

// Don't use inline event handlers.
/*
export default class App extends Component {
  constructor(props) {
    super(props)
  }

  render() {
    return <button onClick={() => alert('Button clicked')}>Click me</button>
  }
}
*/

// Use event listeners and event delegation instead.
export default class App extends Component {
  constructor(props) {
    super(props)
  }

  clickHandler(e) {
    if (e.target.tagName === 'BUTTON') {
      alert('Button clicked')
    }
  }

  componentDidMount() {
    document.addEventListener('click', this.handleClick)
  }

  componentWillUnmount() {
    // Remove event listeners when unmounting the component.
    document.removeEventListener('click', this.handleClick)
  }

  render() {
    return <button onClick={() => alert('Button clicked')}>Click me</button>
  }
}
```
{% endtab %}
{% endtabs %}

Timers are another common resource that should be cleaned up when no longer needed.

```javascript
import React, { useEffect, useState } from 'react'

let timer = null

function StopWatch() {
  const [ms, setMs] = useState(0)
  const [sec, setSec] = useState(0)
  const [min, setMin] = useState(0)
  const [hour, setHour] = useState(0)

  useEffect(() => {
    timer && clearInterval(timer)

    timer = setInterval(() => {
      console.log('Timer is running')

      if (ms + 1 < 999) {
        setMs(ms + 1)
      } else {
        setMs(0)

        if (sec + 1 < 60) {
          setSec(sec + 1)
        } else {
          setSec(0)

          if (min + 1 < 60) {
            setMin(min + 1)
          } else {
            setMin(0)
            setHour(hour + 1)
          }
        }
      }
    }, 1)

    // Uncomment the following line to clean up the timer when unmounting the component.
    //return () => clearInterval(timer)
  })

  return (
    <>
      <p>
        {'Stopwatch is running: '}
        {`${hour < 10 ? '0' : ''}${hour}:`}
        {`${min < 10 ? '0' : ''}${min}:`}
        {`${sec < 10 ? '0' : ''}${sec}.`}
        {`${ms < 10 ? '00' : ms < 100 ? '0' : ''}${ms}`}
      </p>
    </>
  )
}

export default function App() {
  const [unmounted, setUnmounted] = useState(false)

  useEffect(() => {
    function unmountStopWatch(e) {
      if (e.target.tagName === 'BUTTON') {
        setUnmounted(true)
      }
    }

    document.addEventListener('click', unmountStopWatch)

    return () => document.removeEventListener('click', unmountStopWatch)
  }, [])
  return unmounted ? (
    'Open DevTools and see the Console panel'
  ) : (
    <>
      <StopWatch />
      <button>Unmount stopwatch</button>
    </>
  )
}
```

## Not using the key prop

React uses virtual DOM to reduce heavy web browser tasks like painting and recalibrating. Because virtual DOM is just a Javascript object, updating it is direct and fast. Afterward, React uses reconciliation to update the real DOM.

Reconciliation efficiently makes only necessary changes to the real DOM. Below are the basic steps that it follows.

1. Creating a virtual DOM, a copy of the real DOM as a Javascript object.
2. Create a new virtual DOM every time a component's props or state changes.
3. Use a diffing algorithm to inspect the changes between the new virtual DOM and the previous one.

The steps above help determine which elements in the real DOM need to be updated and then update only these elements. The diffing algorithm of React focuses on the following points.

1.  **Elements of different types:**

    The diffing algorithm discards the entire old DOM tree and constructs a new one from scratch when the root elements of the virtual DOM trees have different types.
2. **Elements of the same types:**\
   The diffing algorithm only updates changed attributes of DOM elements and changed props and state of existing React component instances and keeps the same underlying subtrees.
3. **Recursing on children:**\
   When recursing on children of a DOM node, the diffing algorithm iterates over both lists of children at the same time to find the differences.

For the 3rd point, let's consider the following example.

```jsx
// Original DOM.
<ul>
    <li>first</li>
    <li>second</li>
</ul>

// Updated DOM.
<ul>
    <li>zero</li>
    <li>first</li>
    <li>second</li>
</ul>
```

In the example above, because the updated DOM has a new element prepended to the list of children, React will reconstruct the entire list when the diffing algorithm iterates from the first to the last `li` elements of both lists.

As a walkaround for this inefficient process, React introduces the `key` prop. Below is the updated revision of the example above.

```jsx
// Original DOM.
<ul>
    <li key="first">first</li>
    <li key="second">second</li>
</ul>

// Updated DOM.
<ul>
    <li key="zero">zero</li>
    <li key="first">first</li>
    <li key="second">second</li>
</ul>
```

When the `key` prop is provided, the diffing algorithm can compare keys and selectively update only child elements whose keys have been changed. This is the reason React throws a warning to provide keys for items on a list. Therefore, always remember to define key prop when all children of a DOM element are of the same type.

## Not using data caching



## Not using memoization



