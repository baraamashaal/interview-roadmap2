
# 8. `React.memo` vs. `useMemo`

## Quick Revision

`React.memo` and `useMemo` are both used for performance optimization in React, but they are used in different contexts.

*   **`React.memo`:** A higher-order component (HOC) that memoizes a **component**. It prevents a component from re-rendering if its props have not changed.

*   **`useMemo`:** A hook that memoizes a **value**. It is used to avoid expensive calculations on every render.

## Detailed Explanation

### `React.memo`

`React.memo` is a higher-order component that you can wrap around a functional component. It performs a shallow comparison of the component's props. If the props have not changed, React will skip re-rendering the component and reuse the last rendered result.

**When to use `React.memo`:**

*   When you have a component that renders often with the same props.
*   When you have a component that is expensive to render.

By default, `React.memo` only does a shallow comparison of props. If you need more control, you can provide a custom comparison function as a second argument.

### `useMemo`

`useMemo` is a hook that memoizes the result of a function call. It takes a function and a dependency array as arguments. The function is only re-executed if one of the dependencies has changed.

**When to use `useMemo`:**

*   When you have an expensive calculation that you don't want to re-run on every render.
*   When you want to prevent a child component from re-rendering unnecessarily by memoizing the props that are passed to it.

## Code Examples

### `React.memo` Example

```jsx
import React, { useState } from 'react';

const MyComponent = React.memo(({ value }) => {
  console.log('Rendering MyComponent');
  return <div>{value}</div>;
});

function App() {
  const [count, setCount] = useState(0);
  const [otherState, setOtherState] = useState(0);

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Increment Count</button>
      <button onClick={() => setOtherState(otherState + 1)}>Increment Other State</button>
      <MyComponent value={10} />
    </div>
  );
}
```

In this example, `MyComponent` will only render once, even when you click the "Increment Other State" button, because its `value` prop has not changed.

### `useMemo` Example

```jsx
import React, { useState, useMemo } from 'react';

function App() {
  const [count, setCount] = useState(0);
  const [numbers, setNumbers] = useState([1, 2, 3, 4, 5]);

  const expensiveCalculation = (nums) => {
    console.log('Performing expensive calculation...');
    return nums.reduce((acc, current) => acc + current, 0);
  };

  const sum = useMemo(() => expensiveCalculation(numbers), [numbers]);

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Increment Count</button>
      <p>Sum: {sum}</p>
    </div>
  );
}
```

In this example, the `expensiveCalculation` function is only called when the `numbers` array changes, not when the `count` state changes.

## Summary

| Feature      | `React.memo`                             | `useMemo`                                |
|--------------|------------------------------------------|------------------------------------------|
| **Type**     | Higher-Order Component                   | Hook                                     |
| **What it memoizes** | A component                              | A value                                  |
| **Use Case** | Preventing a component from re-rendering | Avoiding expensive calculations          |

## Resources

*   **Article:** [React Docs - `React.memo`](https://reactjs.org/docs/react-api.html#reactmemo)
*   **Article:** [React Docs - `useMemo`](https://reactjs.org/docs/hooks-reference.html#usememo)
*   **Video:** [`React.memo` and `useMemo` - Academind](https://www.youtube.com/watch?v=7_g_N8-x-hE)
