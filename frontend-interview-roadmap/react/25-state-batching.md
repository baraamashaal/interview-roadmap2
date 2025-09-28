
# 25. State Batching in React

## Quick Revision

**State batching** is a performance optimization in React where multiple state updates are grouped together and re-rendered in a single pass. This prevents unnecessary re-renders and improves performance.

*   **React 17 and earlier:** Batching only occurred within React event handlers.
*   **React 18 (Automatic Batching):** Batching now occurs automatically for all updates, including those inside promises, `setTimeout`, and native event handlers.

## Detailed Explanation

When you call `setState` (in class components) or `setSomething` (from `useState` in functional components), React doesn't immediately re-render the component. Instead, it batches these updates.

### Why Batching is Important

Without batching, if you had multiple state updates in a single event handler, each update would trigger a re-render. This would be inefficient and could lead to performance issues.

Batching ensures that React only performs one re-render for multiple state updates, which is much more efficient.

### React 17 and Earlier (Legacy Batching)

In React 17 and earlier, batching only happened in specific scenarios:

*   Inside React event handlers (e.g., `onClick`, `onChange`).
*   During the initial render.

Updates outside of these contexts (e.g., inside `setTimeout`, promises, or native event handlers) would not be batched, leading to multiple re-renders.

```jsx
// React 17 example
function handleClick() {
  setCount(c => c + 1); // Batched
  setFlag(f => !f);     // Batched
  // Only one re-render
}

setTimeout(() => {
  setCount(c => c + 1); // Not batched, causes a re-render
  setFlag(f => !f);     // Not batched, causes another re-render
  // Two re-renders
}, 0);
```

### React 18 (Automatic Batching)

React 18 introduces **automatic batching**, which means that all state updates, regardless of where they originate, are batched together. This significantly improves performance and simplifies state management.

```jsx
// React 18 example
setTimeout(() => {
  setCount(c => c + 1); // Batched
  setFlag(f => !f);     // Batched
  // Only one re-render
}, 0);
```

### Opting Out of Automatic Batching

In rare cases, you might need to opt out of automatic batching. You can do this using `ReactDOM.flushSync()`.

```jsx
import { flushSync } from 'react-dom';

function handleClick() {
  flushSync(() => {
    setCount(c => c + 1);
  });
  // React will re-render here

  flushSync(() => {
    setFlag(f => !f);
  });
  // React will re-render here again
}
```

## Resources

*   **Article:** [React Docs - Automatic Batching for Fewer Renders in React 18](https://reactjs.org/blog/2022/03/08/react-18-upgrade-guide.html#automatic-batching)
*   **Video:** [React 18: Automatic Batching - React Conf 2021](https://www.youtube.com/watch?v=N5R6oX6bLpA)
