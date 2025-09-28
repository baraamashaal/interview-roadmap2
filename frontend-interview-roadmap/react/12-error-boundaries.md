
# 12. Error Boundaries in React

## Quick Revision

**Error boundaries** are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of the component tree that crashed.

Error boundaries are implemented as class components with a `componentDidCatch` lifecycle method and, optionally, a `static getDerivedStateFromError` method.

## Detailed Explanation

By default, if a JavaScript error occurs in a part of the UI, it will cause the entire React component tree to unmount. Error boundaries provide a way to handle these errors gracefully.

### How to Create an Error Boundary

To create an error boundary, you need to create a class component that defines one or both of the following lifecycle methods:

*   **`static getDerivedStateFromError(error)`:** This method is called during the "render" phase, so it does not allow side effects. It should return an object to update the state, which will cause the fallback UI to be rendered.

*   **`componentDidCatch(error, errorInfo)`:** This method is called during the "commit" phase, so it can be used for side effects like logging the error to an external service.

### How to Use an Error Boundary

Once you have created an error boundary component, you can wrap it around any part of your component tree.

```jsx
<ErrorBoundary>
  <MyComponent />
</ErrorBoundary>
```

The error boundary will catch errors in `MyComponent` and any of its children.

### Limitations

Error boundaries do **not** catch errors for:

*   Event handlers
*   Asynchronous code (e.g., `setTimeout` or `requestAnimationFrame` callbacks)
*   Server-side rendering
*   Errors thrown in the error boundary itself

## Code Example

```jsx
import React, { Component } from 'react';

class ErrorBoundary extends Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // Update state so the next render will show the fallback UI.
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // You can also log the error to an error reporting service
    console.error('Uncaught error:', error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      // You can render any custom fallback UI
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children;
  }
}

// Usage
function App() {
  return (
    <div>
      <ErrorBoundary>
        <MyComponentThatMightCrash />
      </ErrorBoundary>
    </div>
  );
}
```

## Resources

*   **Article:** [React Docs - Error Boundaries](https://reactjs.org/docs/error-boundaries.html)
*   **Article:** [Handling Errors in React with Error Boundaries](https://www.freecodecamp.org/news/handling-errors-in-react-with-error-boundaries/)
*   **Video:** [React Error Boundaries - Academind](https://www.youtube.com/watch?v=D_hT-mfRy_s)
