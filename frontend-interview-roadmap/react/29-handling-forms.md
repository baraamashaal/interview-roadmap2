
# 29. Handling Forms in React

## Quick Revision

Handling forms in React involves managing the state of form inputs and responding to user interactions. The most common approach is to use **controlled components**, where React state is the single source of truth for input values.

*   **Controlled Components:** Input values are controlled by React state.
*   **Uncontrolled Components:** Input values are managed by the DOM (less common).
*   **Form Libraries:** Libraries like Formik and React Hook Form simplify form management, validation, and submission.

## Detailed Explanation

### Controlled Components (Recommended)

In a controlled component, the value of the input is driven by React state. This means that every state mutation will have an associated handler function.

**Steps:**

1.  **Initialize state:** Use `useState` to declare a state variable for each input field.
2.  **Bind value:** Set the `value` prop of the input to the corresponding state variable.
3.  **Handle changes:** Attach an `onChange` event handler to update the state whenever the input value changes.

**Benefits:**

*   **Predictable state:** The state is always in sync with the input value.
*   **Easy validation:** You can perform validation on every keystroke.
*   **Centralized control:** All form logic is within your React component.

### Uncontrolled Components

In an uncontrolled component, the form data is handled by the DOM itself. You use a `ref` to get the value of the input when you need it (e.g., on form submission).

**When to use:**

*   For simple forms where you don't need real-time validation or manipulation of input values.
*   When integrating with third-party DOM libraries.

### Form Submission

When the form is submitted, you typically prevent the default browser behavior (`event.preventDefault()`) and then process the form data.

### Form Validation

Form validation can be implemented manually or using form libraries.

*   **Manual validation:** You can add validation logic in your `onChange` handlers or on form submission.
*   **Form libraries:** Libraries like Formik and React Hook Form provide robust validation solutions.

## Code Examples

### Controlled Form Example

```jsx
import React, { useState } from 'react';

function ControlledForm() {
  const [username, setUsername] = useState('');
  const [password, setPassword] = useState('');

  const handleSubmit = (event) => {
    event.preventDefault();
    alert(`Username: ${username}, Password: ${password}`);
    // Here you would typically send the data to a server
  };

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label>
          Username:
          <input
            type="text"
            value={username}
            onChange={(e) => setUsername(e.target.value)}
          />
        </label>
      </div>
      <div>
        <label>
          Password:
          <input
            type="password"
            value={password}
            onChange={(e) => setPassword(e.target.value)}
          />
        </label>
      </div>
      <button type="submit">Login</button>
    </form>
  );
}
```

### Using a Form Library (React Hook Form)

```jsx
import React from 'react';
import { useForm } from 'react-hook-form';

function MyForm() {
  const { register, handleSubmit, formState: { errors } } = useForm();

  const onSubmit = (data) => console.log(data);

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <div>
        <label>Email</label>
        <input
          type="email"
          {...register('email', { required: true, pattern: /.+@.+\..+/i })}
        />
        {errors.email && <span>This field is required and must be a valid email</span>}
      </div>
      <div>
        <label>Password</label>
        <input
          type="password"
          {...register('password', { required: true, minLength: 6 })}
        />
        {errors.password && <span>Password is required and must be at least 6 characters</span>}
      </div>
      <button type="submit">Submit</button>
    </form>
  );
}
```

## Resources

*   **Article:** [React Docs - Forms](https://reactjs.org/docs/forms.html)
*   **Library:** [Formik](https://formik.org/)
*   **Library:** [React Hook Form](https://react-hook-form.com/)
*   **Video:** [React Forms - Academind](https://www.youtube.com/watch?v=Q_f0y-g-200)
