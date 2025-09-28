
# 2. React Lifecycle Methods

## Quick Revision

In class components, React provides a set of lifecycle methods that allow you to run code at specific points in a component's life. The most common lifecycle methods are:

*   **`render()`:** The only required method in a class component. It returns the component's UI.
*   **`componentDidMount()`:** Called after the component is mounted (inserted into the DOM). This is a good place to make API calls or set up subscriptions.
*   **`componentDidUpdate(prevProps, prevState)`:** Called after the component is updated. This is where you can perform side effects based on changes to props or state.
*   **`componentWillUnmount()`:** Called just before the component is unmounted and destroyed. This is where you should clean up any subscriptions or timers.

In functional components, the `useEffect` hook provides the same functionality as these lifecycle methods.

## Detailed Explanation

The component lifecycle can be divided into three phases:

1.  **Mounting:** The component is being created and inserted into the DOM.
2.  **Updating:** The component is being re-rendered as a result of changes to its props or state.
3.  **Unmounting:** The component is being removed from the DOM.

### Mounting

*   **`constructor(props)`:** Called before the component is mounted. This is where you should initialize state and bind event handlers.
*   **`static getDerivedStateFromProps(props, state)`:** A rarely used method that allows a component to update its state based on a change in props.
*   **`render()`:** Renders the component's UI.
*   **`componentDidMount()`:** Called after the component is rendered to the DOM.

### Updating

*   **`static getDerivedStateFromProps(props, state)`:** Called on every re-render.
*   **`shouldComponentUpdate(nextProps, nextState)`:** A performance optimization that allows you to control whether the component should re-render.
*   **`render()`:** Renders the component's UI.
*   **`getSnapshotBeforeUpdate(prevProps, prevState)`:** Called right before the changes from the virtual DOM are to be reflected in the DOM.
*   **`componentDidUpdate(prevProps, prevState, snapshot)`:** Called after the component has been updated in the DOM.

### Unmounting

*   **`componentWillUnmount()`:** Called just before the component is removed from the DOM.

## `useEffect` Hook in Functional Components

The `useEffect` hook is a combination of `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`.

*   **`useEffect(callback, [])`:** The callback runs once, after the initial render (equivalent to `componentDidMount`).
*   **`useEffect(callback, [dep1, dep2])`:** The callback runs after the initial render and whenever any of the dependencies in the array change (equivalent to `componentDidUpdate`).
*   **The cleanup function:** The function returned from the `useEffect` callback is the cleanup function. It runs before the component is unmounted and before the effect runs again (equivalent to `componentWillUnmount`).

## Code Examples

### Class Component Lifecycle

```jsx
import React, { Component } from 'react';

class MyComponent extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  componentDidMount() {
    console.log('Component mounted');
  }

  componentDidUpdate(prevProps, prevState) {
    if (prevState.count !== this.state.count) {
      console.log('Component updated');
    }
  }

  componentWillUnmount() {
    console.log('Component will unmount');
  }

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Increment
        </button>
      </div>
    );
  }
}
```

### Functional Component with `useEffect`

```jsx
import React, { useState, useEffect } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log('Component mounted or updated');

    return () => {
      console.log('Component will unmount or re-run effect');
    };
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

## Resources

*   **Article:** [React Docs - State and Lifecycle](https://reactjs.org/docs/state-and-lifecycle.html)
*   **Article:** [React Docs - `useEffect` Hook](https://reactjs.org/docs/hooks-effect.html)
*   **Diagram:** [React Lifecycle Methods diagram](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)
