
# 26. Dynamic Import in ES6

## Quick Revision

**Dynamic `import()`** is a feature in JavaScript that allows you to load modules on demand. Unlike static `import`, which is processed at compile time, dynamic `import()` is processed at runtime. It returns a `Promise` that resolves to the module object.

This is useful for **code splitting** and **lazy loading**, which can significantly improve the performance of your application by only loading the code that is needed.

## Detailed Explanation

### Static `import`

Static `import` statements are processed before the script is executed. They must be at the top level of your module.

```javascript
import { myFunction } from './myModule.js';

myFunction();
```

This is great for loading essential modules, but it can be inefficient if you have large modules that are not always needed.

### Dynamic `import()`

Dynamic `import()` provides a way to load modules asynchronously.

*   **Syntax:** `import('./myModule.js')`
*   **Returns:** A `Promise` that resolves to the module namespace object.
*   **Usage:** Can be used anywhere in your code, including inside functions and conditional blocks.

## Code Examples

### Basic Dynamic Import

```javascript
// main.js
const button = document.getElementById('myButton');

button.addEventListener('click', () => {
  import('./myModule.js')
    .then(module => {
      module.myFunction();
    })
    .catch(err => {
      console.error('Failed to load module', err);
    });
});

// myModule.js
export function myFunction() {
  console.log('Module loaded and executed!');
}
```

In this example, `myModule.js` is only loaded when the button is clicked.

### With `async/await`

```javascript
button.addEventListener('click', async () => {
  try {
    const module = await import('./myModule.js');
    module.myFunction();
  } catch (err) {
    console.error('Failed to load module', err);
  }
});
```

### Conditional Loading

```javascript
if (isFeatureEnabled) {
  import('./feature.js').then(module => {
    module.initialize();
  });
}
```

## Use Cases

*   **Code Splitting:** Breaking up your code into smaller chunks that can be loaded on demand. This is a key feature of modern web bundlers like Webpack and Rollup.
*   **Lazy Loading:** Delaying the loading of a module until it is actually needed. This is often used for loading components in single-page applications (e.g., when a user navigates to a new route).
*   **Internationalization (i18n):** Loading language packs dynamically based on the user's locale.

## Resources

*   **Article:** [MDN - import()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/import)
*   **Article:** [Dynamic `import()` in JavaScript](https://javascript.info/dynamic-imports)
*   **Article:** [Code-Splitting with Dynamic Imports in React](https://reactjs.org/docs/code-splitting.html#dynamic-import)
