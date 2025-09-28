
# 1. Functional vs. Class Components in React

## Quick Revision

In React, you can create components using either functions or classes.

*   **Class Components:** The original way of writing stateful components in React. They are ES6 classes that extend `React.Component` and have a `render()` method.

*   **Functional Components:** A simpler way to write components. They are just JavaScript functions that accept props and return a React element. With the introduction of **Hooks**, functional components can now have state and lifecycle features, making them the recommended way to write components in modern React.

## Detailed Explanation

### Class Components

*   **State:** State is managed using `this.state` and updated with `this.setState()`.
*   **Lifecycle:** Lifecycle methods like `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` are used to run code at specific points in the component's life.
*   **`this` keyword:** The `this` keyword can be a source of confusion, and you often need to bind event handlers in the constructor.

### Functional Components and Hooks

Functional components were originally stateless, but with the introduction of Hooks in React 16.8, they can now be stateful and have lifecycle features.

*   **State:** The `useState` hook is used to add state to a functional component.
*   **Lifecycle:** The `useEffect` hook is used to perform side effects, which is equivalent to `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` combined.
*   **No `this` keyword:** There is no `this` keyword in functional components, which makes the code simpler and easier to read.

### Key Differences

| Feature      | Class Components                       | Functional Components                  |
|--------------|----------------------------------------|----------------------------------------|
| **Syntax**   | More verbose (ES6 class)               | More concise (JavaScript function)     |
| **State**    | `this.state`, `this.setState()`        | `useState` hook                        |
| **Lifecycle**| Lifecycle methods                      | `useEffect` hook                       |
| **`this`**   | Can be confusing                       | No `this` keyword                      |
| **Recommendation** | Legacy (still supported)               | Recommended for new code               |

## Code Examples

### Class Component Example

```jsx
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}
```

### Functional Component Example

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

## Why Functional Components are Preferred

*   **Simpler to read and write:** Less boilerplate code.
*   **Easier to test:** They are just functions, so they are easier to test in isolation.
*   **Better performance:** In some cases, functional components can be more performant.
*   **Hooks:** Hooks provide a more elegant and powerful way to handle state and side effects.

## Resources

*   **Article:** [React Docs - Components and Props](https://reactjs.org/docs/components-and-props.html)
*   **Article:** [React Docs - Introducing Hooks](https://reactjs.org/docs/hooks-intro.html)
*   **Video:** [React Functional Components vs. Class Components - Academind](https://www.youtube.com/watch?v=l_h9I-43-gI)
