
# 19. Custom Hooks in React

## Quick Revision

A **custom Hook** is a JavaScript function whose name starts with `use` and that calls other Hooks. It is a way to extract component logic into a reusable function.

Custom Hooks allow you to share stateful logic between components without having to use higher-order components or render props.

## Detailed Explanation

### Why Use Custom Hooks?

Custom Hooks solve the problem of code duplication. If you have two components that share the same stateful logic, you can extract that logic into a custom Hook and reuse it in both components.

### Creating a Custom Hook

A custom Hook is just a regular JavaScript function with two key characteristics:

1.  Its name must start with `use` (e.g., `useFormInput`, `useFetch`).
2.  It can call other Hooks (e.g., `useState`, `useEffect`).

## Code Example

Let's say you have a form with several input fields, and you want to manage the state of each input. You could write the same `useState` logic for each input, but that would be repetitive.

Instead, you can create a custom Hook called `useFormInput`:

```jsx
import { useState } from 'react';

function useFormInput(initialValue) {
  const [value, setValue] = useState(initialValue);

  const handleChange = (e) => {
    setValue(e.target.value);
  };

  return {
    value,
    onChange: handleChange
  };
}
```

Now you can use this custom Hook in your components:

```jsx
import React from 'react';
import useFormInput from './useFormInput';

function MyForm() {
  const firstName = useFormInput('');
  const lastName = useFormInput('');

  return (
    <form>
      <input type="text" {...firstName} />
      <input type="text" {...lastName} />
    </form>
  );
}
```

### Another Example: `useFetch`

Here is a custom Hook for fetching data from an API:

```jsx
import { useState, useEffect } from 'react';

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    setLoading(true);
    fetch(url)
      .then(response => response.json())
      .then(data => {
        setData(data);
        setLoading(false);
      })
      .catch(error => {
        setError(error);
        setLoading(false);
      });
  }, [url]);

  return { data, loading, error };
}
```

And here is how you would use it:

```jsx
import React from 'react';
import useFetch from './useFetch';

function UserProfile({ userId }) {
  const { data: user, loading, error } = useFetch(`https://api.example.com/users/${userId}`);

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error!</div>;

  return <div>{user.name}</div>;
}
```

## Resources

*   **Article:** [React Docs - Building Your Own Hooks](https://reactjs.org/docs/hooks-custom.html)
*   **Video:** [React Custom Hooks - Academind](https://www.youtube.com/watch?v=J-g9ZJha8FE)
*   **Collection:** [A collection of useful React custom Hooks](https://github.com/streamich/react-use)
