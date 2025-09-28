
# 15. React Hydration

## Quick Revision

**Hydration** is the process of attaching React to a DOM that was already rendered by the server. In a server-side rendered (SSR) application, the server sends a fully rendered HTML page to the browser. React then "hydrates" this HTML by attaching event listeners and making the application interactive.

It is the process that happens on the client-side after the server has rendered the initial HTML.

## Detailed Explanation

In a typical server-side rendering setup:

1.  The server renders the React components to an HTML string and sends it to the client.
2.  The client receives the HTML and displays it to the user.
3.  The client then downloads the JavaScript bundle.
4.  React runs on the client and, instead of re-rendering the entire application, it "hydrates" the existing server-rendered HTML.

### `ReactDOM.hydrateRoot()`

In React 18, `ReactDOM.hydrateRoot()` is the new API for hydrating a server-rendered application. It takes two arguments:

1.  The DOM element to hydrate.
2.  The React element to render.

```jsx
// client.js
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';

const rootElement = document.getElementById('root');
ReactDOM.hydrateRoot(rootElement, <App />);
```

### How Hydration Works

During hydration, React will try to attach event listeners to the existing markup. It expects that the server-rendered content is identical to what it would render on the client. If there are any mismatches, React will warn you during development, but it will not attempt to patch up the differences.

### Benefits of Hydration

*   **Performance:** Hydration is generally faster than rendering the entire application from scratch on the client.
*   **User Experience:** The user sees the content of the page faster, and the application becomes interactive once the JavaScript has loaded.

## Common Issues

*   **"Text content does not match server-rendered HTML" warning:** This warning occurs when the content rendered on the client is different from the content rendered on the server. This can be caused by things like:
    *   Using `new Date()` or `Math.random()` in your components.
    *   Rendering different content based on the user agent.

## Resources

*   **Article:** [React Docs - `ReactDOM.hydrateRoot`](https://reactjs.org/docs/react-dom-client.html#hydrateroot)
*   **Article:** [Fixing the "Text content does not match server-rendered HTML" Error in React](https://www.freecodecamp.org/news/fixing-the-text-content-does-not-match-server-rendered-html-error-in-react/)
*   **Video:** [What is React Hydration? - Academind](https://www.youtube.com/watch?v=Nq_Qd_G-iA8)
