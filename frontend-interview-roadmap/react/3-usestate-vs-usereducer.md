
# 3. `useState` vs. `useReducer` in React

## Quick Revision

`useState` and `useReducer` are both hooks used for managing state in React functional components.

*   **`useState`:** The basic hook for managing simple state. It takes the initial state as an argument and returns an array with the current state and a function to update it.

*   **`useReducer`:** An alternative to `useState` for managing more complex state logic. It is inspired by Redux and uses a reducer function to update the state based on dispatched actions.

## Detailed Explanation

### `useState`

`useState` is the go-to hook for managing simple state, such as a boolean, a string, or a number.

**When to use `useState`:**

*   When you have simple state.
*   When the state logic is straightforward.

### `useReducer`

`useReducer` is a better choice for managing complex state that involves multiple sub-values or when the next state depends on the previous one.

`useReducer` takes a reducer function and an initial state as arguments and returns an array with the current state and a `dispatch` function.

**The reducer function:**

*   Takes the current state and an action as arguments.
*   Returns the new state.
*   ` (state, action) => newState `

**The `dispatch` function:**

*   Takes an action object as an argument.
*   Triggers a state update by calling the reducer function.

**When to use `useReducer`:**

*   When you have complex state logic.
*   When the next state depends on the previous one.
*   When you want to optimize performance for components that trigger deep updates, as you can pass down a `dispatch` function instead of callbacks.

## Code Examples

### `useState` Example

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={() => setCount(count - 1)}>Decrement</button>
    </div>
  );
}
```

### `useReducer` Example

```jsx
import React, { useReducer } from 'react';

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
    </div>
  );
}
```

## Summary

| Feature      | `useState`                               | `useReducer`                             |
|--------------|------------------------------------------|------------------------------------------|
| **Best for** | Simple state                             | Complex state                            |
| **State Logic**| Contained within the component           | Centralized in a reducer function        |
| **Performance**| Can cause re-renders if not used carefully | Can optimize performance with `dispatch` |

## Resources

*   **Article:** [React Docs - `useState`](https://reactjs.org/docs/hooks-reference.html#usestate)
*   **Article:** [React Docs - `useReducer`](https://reactjs.org/docs/hooks-reference.html#usereducer)
*   **Article:** [When to use `useState` vs. `useReducer`](https://kentcdodds.com/blog/should-i-usestate-or-usereducer)
