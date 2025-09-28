
# 18. The Rules of Hooks in React

## Quick Revision

Hooks are a powerful feature in React, but they have two important rules that you must follow to ensure they work correctly.

1.  **Only Call Hooks at the Top Level:** Don’t call Hooks inside loops, conditions, or nested functions. Always use Hooks at the top level of your React function.

2.  **Only Call Hooks from React Functions:** Don’t call Hooks from regular JavaScript functions. You can only call Hooks from React functional components or from custom Hooks.

## Detailed Explanation

### Rule 1: Only Call Hooks at the Top Level

React relies on the order in which Hooks are called to associate the state of a Hook with a particular component. If you call a Hook inside a condition, the order of the Hooks can change between renders, which can lead to bugs.

**Incorrect:**

```jsx
function MyComponent({ hasName }) {
  if (hasName) {
    const [name, setName] = useState('Baraa'); // Incorrect: called inside a condition
  }

  const [age, setAge] = useState(30);

  // ...
}
```

**Correct:**

```jsx
function MyComponent({ hasName }) {
  const [name, setName] = useState(hasName ? 'Baraa' : '');
  const [age, setAge] = useState(30);

  // ...
}
```

### Rule 2: Only Call Hooks from React Functions

You can only call Hooks from:

*   **React functional components:**

    ```jsx
    function MyComponent() {
      const [name, setName] = useState('Baraa'); // Correct
      // ...
    }
    ```

*   **Custom Hooks:** A custom Hook is a JavaScript function whose name starts with `use` and that calls other Hooks.

    ```jsx
    function useFormInput(initialValue) {
      const [value, setValue] = useState(initialValue); // Correct
      // ...
      return { value, onChange: e => setValue(e.target.value) };
    }
    ```

**Incorrect:**

```javascript
function myHelperFunction() {
  const [value, setValue] = useState(''); // Incorrect: not a React function
}
```

## Linting

React provides an ESLint plugin called `eslint-plugin-react-hooks` that automatically enforces these two rules. It is included by default in Create React App.

## Resources

*   **Article:** [React Docs - Rules of Hooks](https://reactjs.org/docs/hooks-rules.html)
*   **Video:** [The Rules of Hooks - React Conf 2018](https://www.youtube.com/watch?v=dpw9EHDh2bM)
