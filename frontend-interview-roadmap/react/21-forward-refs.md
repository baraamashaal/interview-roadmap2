
# 21. Forwarding Refs in React

## Quick Revision

**Ref forwarding** is a technique for automatically passing a `ref` through a component to one of its children. This is particularly useful when building reusable component libraries or higher-order components.

It allows a parent component to pass a `ref` to a child component, which can then forward it to an underlying DOM element or another component.

## Detailed Explanation

Refs provide a way to access DOM nodes or React elements created in the render method. However, you cannot directly attach a ref to a functional component because functional components don't have instances.

### The Problem

Consider a higher-order component (HOC) that wraps another component. If you try to attach a ref to the HOC, you will get a ref to the HOC itself, not to the wrapped component or its underlying DOM element.

### The Solution: `React.forwardRef()`

`React.forwardRef()` is a function that lets you pass a `ref` down to a child component. It takes a render function as an argument. This render function receives `props` and `ref` as its arguments.

```jsx
const MyFunctionalComponent = React.forwardRef((props, ref) => (
  <input ref={ref} {...props} />
));
```

Now, when a parent component uses `MyFunctionalComponent` and passes a `ref` to it, that `ref` will be forwarded to the underlying `<input>` element.

## Code Example

### Without Ref Forwarding (Problem)

```jsx
import React, { useRef } from 'react';

function MyInput(props) {
  return <input {...props} />;
}

function App() {
  const inputRef = useRef(null);

  const handleClick = () => {
    inputRef.current.focus(); // This will not work, inputRef.current is null
  };

  return (
    <div>
      <MyInput ref={inputRef} />
      <button onClick={handleClick}>Focus Input</button>
    </div>
  );
  // Warning: Function components cannot be given refs. Attempts to access this ref will fail.
}
```

### With Ref Forwarding (Solution)

```jsx
import React, { useRef, forwardRef } from 'react';

const MyInput = forwardRef((props, ref) => {
  return <input ref={ref} {...props} />;
});

function App() {
  const inputRef = useRef(null);

  const handleClick = () => {
    inputRef.current.focus(); // This will now work
  };

  return (
    <div>
      <MyInput ref={inputRef} />
      <button onClick={handleClick}>Focus Input</button>
    </div>
  );
}
```

## Use Cases

*   **Reusable Component Libraries:** When you are building a component library, you often want to allow users to attach refs to your components.
*   **Higher-Order Components (HOCs):** HOCs often wrap other components, and ref forwarding allows you to pass refs through the HOC to the wrapped component.
*   **Integrating with Third-Party DOM Libraries:** When you need to interact with a third-party library that expects a DOM element.

## Resources

*   **Article:** [React Docs - Forwarding Refs](https://reactjs.org/docs/forwarding-refs.html)
*   **Video:** [React Ref Forwarding - Academind](https://www.youtube.com/watch?v=Sc_gXf0g_1Q)
