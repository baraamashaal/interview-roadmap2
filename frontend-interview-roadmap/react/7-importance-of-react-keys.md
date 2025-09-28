
# 7. The Importance of Keys in React

## Quick Revision

**Keys** are a special string attribute you need to include when creating lists of elements in React. They help React identify which items have changed, been added, or been removed. This allows React to efficiently update the UI.

Keys should be **stable, predictable, and unique** for each element in a list.

## Detailed Explanation

When you render a list of elements, React's reconciliation algorithm needs a way to match the elements in the new virtual DOM tree with the elements in the old one. Keys provide this mapping.

### Why are Keys Important?

Without keys, React would have to rely on the order of the elements to determine which ones have changed. This can be inefficient and can lead to unexpected behavior, especially if the order of the elements can change.

Consider a list where you are adding a new item to the beginning:

*   **Without keys:** React will see that the first element has changed, the second element has changed, and so on. It will re-render all the elements in the list.
*   **With keys:** React will see that there is a new element with a new key, and it will only render that new element.

### Choosing a Key

*   **Best option:** A unique, stable ID from your data (e.g., a database ID).

    ```jsx
    const todoItems = todos.map(todo =>
      <li key={todo.id}>
        {todo.text}
      </li>
    );
    ```

*   **Last resort:** The index of the element in the array. This is not recommended if the order of the items can change, as it can lead to performance issues and bugs with component state.

    ```jsx
    const todoItems = todos.map((todo, index) =>
      // Only do this if the items have no stable IDs
      <li key={index}>
        {todo.text}
      </li>
    );
    ```

### Where to Use Keys

Keys should be specified on the top-level element in a list.

```jsx
// Correct
const todoItems = todos.map(todo =>
  <li key={todo.id}>
    {todo.text}
  </li>
);

// Incorrect
const todoItems = todos.map(todo =>
  <div key={todo.id}>
    <li>{todo.text}</li>
  </div>
);
```

## Code Example

### Incorrect: Using Index as a Key with a Sortable List

```jsx
import React, { useState } from 'react';

function UnstableList() {
  const [items, setItems] = useState([
    { id: 1, text: 'Item 1' },
    { id: 2, text: 'Item 2' },
  ]);

  const handleSort = () => {
    setItems([...items].reverse());
  };

  return (
    <div>
      <button onClick={handleSort}>Sort</button>
      <ul>
        {items.map((item, index) => (
          <li key={index}>{item.text} <input type="text" /></li>
        ))}
      </ul>
    </div>
  );
}
```

In this example, if you type something into the input field of the first item and then click "Sort", the text you typed will stay in the first input field, even though the item has moved. This is because React is using the index as the key, and it thinks that only the text of the `<li>` has changed, not the `<li>` itself.

### Correct: Using a Stable ID as a Key

```jsx
// ...
<ul>
  {items.map(item => (
    <li key={item.id}>{item.text} <input type="text" /></li>
  ))}
</ul>
// ...
```

With a stable key, React will correctly identify that the items have been reordered, and the input fields will move with their corresponding items.

## Resources

*   **Article:** [React Docs - Lists and Keys](https://reactjs.org/docs/lists-and-keys.html)
*   **Article:** [React Docs - Reconciliation (The Power of Keys)](https://reactjs.org/docs/reconciliation.html#the-power-of-keys)
*   **Video:** [React Keys - Academind](https://www.youtube.com/watch?v=5sQ1iZ_i_Jc)
