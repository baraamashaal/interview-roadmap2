
# 4. `useEffect` Explained

## Quick Revision

The **`useEffect`** hook lets you perform **side effects** in functional components. Side effects are any operations that affect something outside of the component, such as:

*   Fetching data from an API
*   Setting up subscriptions (e.g., to a WebSocket)
*   Manually changing the DOM
*   Setting timers (`setTimeout`, `setInterval`)

`useEffect` is a combination of `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` from class components.

## Detailed Explanation

The `useEffect` hook takes two arguments:

1.  **A callback function:** This is where you put your side effect code.
2.  **A dependency array (optional):** This is an array of values that the effect depends on.

### The Dependency Array

The dependency array controls when the effect is run.

*   **No dependency array:** The effect runs after **every** render.

    ```jsx
    useEffect(() => {
      console.log('Component rendered');
    });
    ```

*   **Empty dependency array (`[]`):** The effect runs **only once**, after the initial render. This is equivalent to `componentDidMount`.

    ```jsx
    useEffect(() => {
      console.log('Component mounted');
    }, []);
    ```

*   **Dependency array with values (`[dep1, dep2]`):** The effect runs after the initial render and whenever any of the values in the dependency array change. This is equivalent to `componentDidUpdate`.

    ```jsx
    useEffect(() => {
      console.log(`The value of myProp has changed to: ${myProp}`);
    }, [myProp]);
    ```

### The Cleanup Function

The function returned from the `useEffect` callback is the **cleanup function**. It is used to clean up any resources created by the effect, such as subscriptions or timers.

The cleanup function runs:

*   Before the component is unmounted.
*   Before the effect runs again.

This is equivalent to `componentWillUnmount`.

## Code Examples

### Fetching Data

```jsx
import React, { useState, useEffect } from 'react';

function UserProfile({ userId }) {
  const [user, setUser] = useState(null);

  useEffect(() => {
    fetch(`https://api.example.com/users/${userId}`)
      .then(response => response.json())
      .then(data => setUser(data));
  }, [userId]); // Re-run the effect if userId changes

  if (!user) {
    return <div>Loading...</div>;
  }

  return <div>{user.name}</div>;
}
```

### Setting up a Timer

```jsx
import React, { useState, useEffect } from 'react';

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const intervalId = setInterval(() => {
      setSeconds(s => s + 1);
    }, 1000);

    // Cleanup function
    return () => {
      clearInterval(intervalId);
    };
  }, []); // Run only once

  return <div>Seconds: {seconds}</div>;
}
```

## Rules of Hooks

*   Only call hooks at the top level of your functional components.
*   Only call hooks from React functions.

## Resources

*   **Article:** [React Docs - `useEffect` Hook](https://reactjs.org/docs/hooks-effect.html)
*   **Article:** [A Complete Guide to `useEffect`](https://overreacted.io/a-complete-guide-to-useeffect/)
*   **Video:** [React `useEffect` Hook - Academind](https://www.youtube.com/watch?v=0ZJg_IeYgwQ)
