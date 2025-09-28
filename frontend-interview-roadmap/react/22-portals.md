
# 22. Portals in React

## Quick Revision

**Portals** provide a way to render children into a DOM node that exists outside the DOM hierarchy of the parent component. This is useful for components like modals, tooltips, and popovers that need to be rendered outside the normal component tree to avoid issues with z-index, overflow, or positioning.

## Detailed Explanation

Normally, when you return an element from a component's `render` method, it is mounted into the DOM as a child of the nearest parent DOM node. However, with portals, you can render a child into a different part of the DOM tree.

### How to Use Portals

1.  **Create a DOM element outside the root of your React application.** This is typically done in `index.html`.

    ```html
    <div id="root"></div>
    <div id="modal-root"></div>
    ```

2.  **Use `ReactDOM.createPortal()` to render a component into that DOM element.**

    ```jsx
    ReactDOM.createPortal(child, container)
    ```

    *   `child`: Any renderable React child (e.g., an element, string, or fragment).
    *   `container`: A DOM element.

### Event Bubbling

Even though a portal's children are rendered into a different DOM node, they still behave like normal React children in terms of event bubbling. Events fired from inside a portal will propagate up to the parent components in the React tree, even if those components are not ancestors in the DOM tree.

## Code Example

```jsx
import React, { useState } from 'react';
import ReactDOM from 'react-dom';

// Create a DOM element for the modal outside the root
// (This would typically be in your public/index.html)
// const modalRoot = document.getElementById('modal-root');

function Modal({ children }) {
  const modalRoot = document.getElementById('modal-root');
  return ReactDOM.createPortal(
    <div className="modal-backdrop">
      <div className="modal-content">
        {children}
      </div>
    </div>,
    modalRoot
  );
}

function App() {
  const [showModal, setShowModal] = useState(false);

  const handleShow = () => setShowModal(true);
  const handleHide = () => setShowModal(false);

  return (
    <div>
      <h1>My App</h1>
      <button onClick={handleShow}>Show Modal</button>

      {showModal && (
        <Modal>
          <h2>This is a Modal</h2>
          <p>Content of the modal goes here.</p>
          <button onClick={handleHide}>Close</button>
        </Modal>
      )}
    </div>
  );
}

export default App;
```

And in your `index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>React Portals Example</title>
</head>
<body>
    <div id="root"></div>
    <div id="modal-root"></div> <!-- This is where the modal will be rendered -->
    <script src="index.js"></script>
</body>
</html>
```

## Use Cases

*   **Modals, Dialogs, Popups:** These components often need to be rendered on top of everything else, regardless of their parent's `z-index` or `overflow` properties.
*   **Tooltips and Context Menus:** Similar to modals, these often need to break out of their parent's layout.

## Resources

*   **Article:** [React Docs - Portals](https://reactjs.org/docs/portals.html)
*   **Video:** [React Portals - Academind](https://www.youtube.com/watch?v=A_yX_0-1_0Q)
