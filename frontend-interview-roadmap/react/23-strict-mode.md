
# 23. Strict Mode in React

## Quick Revision

**`StrictMode`** is a tool for highlighting potential problems in a React application. Like `Fragment`, `StrictMode` does not render any visible UI. It activates additional checks and warnings for its descendants.

It helps you write better React code by identifying unsafe lifecycles, legacy API usage, and other potential issues.

## Detailed Explanation

`StrictMode` is a development-only tool. It does not affect the production build of your application. It is designed to help you catch bugs and potential problems early in the development process.

### What `StrictMode` Does

`StrictMode` currently helps with:

1.  **Identifying components with unsafe lifecycles:** It warns about legacy lifecycle methods that are prone to bugs, especially with concurrent rendering.
2.  **Warning about legacy string ref API usage:** It encourages the use of `createRef()` or `useRef()`.
3.  **Warning about deprecated findDOMNode usage:** `findDOMNode` is a legacy API that is discouraged.
4.  **Detecting unexpected side effects:** It intentionally double-invokes certain functions (like `render`, `useState` setters, `useEffect` cleanup) in development to help you find side effects that might cause problems in concurrent mode.
5.  **Detecting legacy context API usage:** It warns about the old context API, encouraging the use of `React.createContext()` and `useContext()`.

### How to Use `StrictMode`

You can enable `StrictMode` for any part of your application. It will apply to all of its descendants.

```jsx
import React from 'react';

function App() {
  return (
    <React.StrictMode>
      <MyComponent />
    </React.StrictMode>
  );
}
```

## Code Example

Consider a component that uses a legacy lifecycle method:

```jsx
import React, { Component } from 'react';

class MyLegacyComponent extends Component {
  // This lifecycle method is considered unsafe in StrictMode
  componentWillMount() {
    console.log('componentWillMount');
  }

  render() {
    return <div>Hello from Legacy Component</div>;
  }
}

function App() {
  return (
    <React.StrictMode>
      <MyLegacyComponent />
    </React.StrictMode>
  );
}
```

When you run this code in development with `StrictMode` enabled, you will see a warning in the console about `componentWillMount` being an unsafe lifecycle method.

### Detecting Unexpected Side Effects

`StrictMode` will intentionally double-invoke certain functions to help you find side effects. For example, if you have a `useEffect` that doesn't have a proper cleanup function, `StrictMode` will run the effect twice to highlight the issue.

```jsx
import React, { useEffect, useState } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log('Effect ran');
    // If you don't have a cleanup function, this will run twice in StrictMode
    // and might cause issues if it's not idempotent.

    return () => {
      console.log('Effect cleanup');
    };
  }, []);

  return <div>Count: {count}</div>;
}

function App() {
  return (
    <React.StrictMode>
      <MyComponent />
    </React.StrictMode>
  );
}
```

In `StrictMode`, you will see "Effect ran" and "Effect cleanup" logged twice on mount, helping you ensure your effects are robust.

## Resources

*   **Article:** [React Docs - StrictMode](https://reactjs.org/docs/strict-mode.html)
*   **Video:** [React StrictMode - Academind](https://www.youtube.com/watch?v=0ZJg_IeYgwQ)
