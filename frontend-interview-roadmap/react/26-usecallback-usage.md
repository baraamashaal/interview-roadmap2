
# 26. `useCallback` Usage in React

## Quick Revision

**`useCallback`** is a React Hook that returns a memoized callback function. It is used to prevent unnecessary re-renders of child components that rely on reference equality for their props.

It takes a function and a dependency array as arguments. The function is only re-created if one of the dependencies has changed.

## Detailed Explanation

In JavaScript, functions are objects. When a component re-renders, any functions defined within that component are re-created. This means that if you pass a function as a prop to a child component, that child component will re-render, even if the function's logic hasn't changed, because the function itself is a new object (a new reference).

This can be a performance issue, especially if the child component is expensive to render.

### How `useCallback` Works

`useCallback` memoizes the function itself. It returns a memoized version of the callback function that only changes if one of the dependencies has changed.

```jsx
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b], // Dependencies
);
```

### When to Use `useCallback`

*   **Passing callbacks to memoized child components:** If you have a child component that is wrapped in `React.memo` (or is a `PureComponent`), and you are passing a callback function as a prop, `useCallback` can prevent unnecessary re-renders of the child component.
*   **Optimizing `useEffect` dependencies:** If a function is a dependency of `useEffect`, and that function is re-created on every render, it can cause the `useEffect` to run unnecessarily. `useCallback` can help here.

## Code Examples

### Without `useCallback` (Problem)

```jsx
import React, { useState } from 'react';

const ChildComponent = React.memo(({ onClick }) => {
  console.log('ChildComponent rendered');
  return <button onClick={onClick}>Click me</button>;
});

function ParentComponent() {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <p>Count: {count}</p>
      <ChildComponent onClick={handleClick} />
    </div>
  );
}
```

In this example, `ChildComponent` will re-render every time `ParentComponent` re-renders, even though its `onClick` prop's logic hasn't changed, because `handleClick` is a new function reference on each render.

### With `useCallback` (Solution)

```jsx
import React, { useState, useCallback } from 'react';

const ChildComponent = React.memo(({ onClick }) => {
  console.log('ChildComponent rendered');
  return <button onClick={onClick}>Click me</button>;
});

function ParentComponent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    setCount(count + 1);
  }, [count]); // Dependency array: re-create handleClick only if count changes

  return (
    <div>
      <p>Count: {count}</p>
      <ChildComponent onClick={handleClick} />
    </div>
  );
}
```

Now, `ChildComponent` will only re-render when the `count` state changes, because `handleClick` maintains the same reference across renders as long as `count` doesn't change.

## Important Considerations

*   **Don't overuse `useCallback`:** It adds a small overhead. Only use it when you have a performance problem or when passing callbacks to memoized child components.
*   **Correct dependency array:** Ensure your dependency array is correct. If you omit a dependency, your memoized function might use a stale value.

## Resources

*   **Article:** [React Docs - `useCallback`](https://reactjs.org/docs/hooks-reference.html#usecallback)
*   **Article:** [When to use `useCallback` and `useMemo`](https://kentcdodds.com/blog/usememo-and-usecallback)
*   **Video:** [React `useCallback` Hook - Academind](https://www.youtube.com/watch?v=l_h9I-43-gI)
