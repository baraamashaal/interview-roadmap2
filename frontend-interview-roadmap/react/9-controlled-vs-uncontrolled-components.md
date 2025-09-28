
# 9. Controlled vs. Uncontrolled Components in React

## Quick Revision

In React, form elements like `<input>`, `<textarea>`, and `<select>` can be either **controlled** or **uncontrolled**.

*   **Controlled Components:** The state of the form element is controlled by React. The value of the input is stored in the component's state, and it is updated via an `onChange` event handler.

*   **Uncontrolled Components:** The state of the form element is managed by the DOM itself. You can get the value of the input using a `ref`.

## Detailed Explanation

### Controlled Components

In a controlled component, the value of the input is driven by the component's state. This is the recommended way to handle forms in React.

**How it works:**

1.  The `value` of the input is set to a value from the component's state.
2.  An `onChange` event handler is used to update the state whenever the user types in the input.

**Benefits:**

*   The component's state is the single source of truth.
*   You can easily validate the input and perform other actions on every keystroke.

### Uncontrolled Components

In an uncontrolled component, the DOM manages the state of the form element. You can use a `ref` to get the value of the input when you need it (e.g., when the form is submitted).

**When to use uncontrolled components:**

*   For simple forms where you don't need to do anything with the input on every keystroke.
*   When integrating with non-React code.
*   For managing file inputs, as their value can only be set by the user.

## Code Examples

### Controlled Component Example

```jsx
import React, { useState } from 'react';

function ControlledForm() {
  const [name, setName] = useState('');

  const handleSubmit = (event) => {
    event.preventDefault();
    alert(`A name was submitted: ${name}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input type="text" value={name} onChange={e => setName(e.target.value)} />
      </label>
      <input type="submit" value="Submit" />
    </form>
  );
}
```

### Uncontrolled Component Example

```jsx
import React, { useRef } from 'react';

function UncontrolledForm() {
  const inputRef = useRef(null);

  const handleSubmit = (event) => {
    event.preventDefault();
    alert(`A name was submitted: ${inputRef.current.value}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input type="text" ref={inputRef} />
      </label>
      <input type="submit" value="Submit" />
    </form>
  );
}
```

## Summary

| Feature      | Controlled Components                    | Uncontrolled Components                  |
|--------------|------------------------------------------|------------------------------------------|
| **State**    | Managed by React                         | Managed by the DOM                       |
| **Data Flow**| Unidirectional (state -> view -> state)  | Bidirectional (DOM -> ref)               |
| **Use Case** | Most forms                               | Simple forms, file inputs                |

## Resources

*   **Article:** [React Docs - Controlled Components](https://reactjs.org/docs/forms.html#controlled-components)
*   **Article:** [React Docs - Uncontrolled Components](https://reactjs.org/docs/uncontrolled-components.html)
*   **Video:** [Controlled vs. Uncontrolled Components - Academind](https://www.youtube.com/watch?v=p_t-l9-t-wA)
