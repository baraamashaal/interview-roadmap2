
# 5. Context API vs. Redux

## Quick Revision

Both the **Context API** and **Redux** are used for state management in React, but they have different use cases and levels of complexity.

*   **Context API:** A built-in feature in React that allows you to share state between components without having to pass props down through the component tree. It is a good solution for managing simple, low-frequency state updates.

*   **Redux:** A third-party library that provides a more powerful and predictable way to manage application state. It is a good choice for large-scale applications with complex state logic.

## Detailed Explanation

### Context API

The Context API is designed to solve the problem of **prop drilling**, which is the process of passing props down through multiple levels of components.

**Key Concepts:**

*   **`React.createContext()`:** Creates a context object.
*   **`Provider`:** A component that provides the context value to its children.
*   **`Consumer` or `useContext` hook:** A component or hook that consumes the context value.

**When to use the Context API:**

*   For simple state that needs to be shared by a few components.
*   For low-frequency updates (e.g., theme, user authentication).

**Limitations:**

*   Can cause performance issues if the context value changes frequently, as all components that consume the context will re-render.
*   Does not provide built-in support for middleware or other advanced features.

### Redux

Redux is a predictable state container for JavaScript apps. It is based on the principles of functional programming and provides a centralized store for your application's state.

**Key Concepts:**

*   **Store:** A single, centralized object that holds the application state.
*   **Actions:** Plain JavaScript objects that describe what happened.
*   **Reducers:** Pure functions that take the current state and an action and return the new state.

**When to use Redux:**

*   For large-scale applications with complex state.
*   When you need a centralized and predictable way to manage state.
*   When you need advanced features like middleware (for logging, async actions, etc.) and time-travel debugging.

**Modern Redux with Redux Toolkit:**

**Redux Toolkit** is the official, recommended way to write Redux logic. It simplifies Redux development by providing a set of utilities that handle common use cases, such as setting up the store, creating reducers, and handling immutable updates.

## Code Examples

### Context API Example

```jsx
// ThemeContext.js
import React, { createContext, useState } from 'react';

export const ThemeContext = createContext();

export const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState('light');

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
};

// MyComponent.js
import React, { useContext } from 'react';
import { ThemeContext } from './ThemeContext';

function MyComponent() {
  const { theme, setTheme } = useContext(ThemeContext);

  return (
    <div className={theme}>
      <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>
        Toggle Theme
      </button>
    </div>
  );
}
```

### Redux Toolkit Example

```jsx
// counterSlice.js
import { createSlice } from '@reduxjs/toolkit';

export const counterSlice = createSlice({
  name: 'counter',
  initialState: { value: 0 },
  reducers: {
    increment: state => {
      state.value += 1;
    },
    decrement: state => {
      state.value -= 1;
    }
  }
});

export const { increment, decrement } = counterSlice.actions;
export default counterSlice.reducer;

// store.js
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from './counterSlice';

export default configureStore({
  reducer: {
    counter: counterReducer
  }
});

// MyComponent.js
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { increment, decrement } from './counterSlice';

function MyComponent() {
  const count = useSelector(state => state.counter.value);
  const dispatch = useDispatch();

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => dispatch(increment())}>Increment</button>
      <button onClick={() => dispatch(decrement())}>Decrement</button>
    </div>
  );
}
```

## Summary

| Feature      | Context API                              | Redux                                    |
|--------------|------------------------------------------|------------------------------------------|
| **Complexity** | Simple                                   | More complex (but simplified by Redux Toolkit) |
| **Use Case** | Simple, low-frequency state updates      | Complex, high-frequency state updates    |
| **DevTools** | Limited                                  | Powerful (time-travel debugging)         |
| **Middleware**| No                                       | Yes                                      |

## Resources

*   **Article:** [React Docs - Context](https://reactjs.org/docs/context.html)
*   **Article:** [Redux Toolkit Documentation](https://redux-toolkit.js.org/)
*   **Video:** [React Context vs. Redux - Academind](https://www.youtube.com/watch?v=F_084-jKL3M)
