
# 20. Performance Tuning in React

## Quick Revision

**Performance tuning** in React involves optimizing your components and application to render faster and use fewer resources. Key strategies include:

*   **Memoization:** Using `React.memo`, `useMemo`, and `useCallback` to prevent unnecessary re-renders and expensive calculations.
*   **Code Splitting:** Loading only the necessary code for a given view.
*   **Virtualization/Windowing:** Rendering only the visible parts of a long list.
*   **Lazy Loading:** Loading components only when they are needed.
*   **Optimizing Images:** Using appropriate image formats and sizes.
*   **Using the Production Build:** React's development build includes extra warnings and debugging tools that are not present in the production build.

## Detailed Explanation

### 1. Memoization (`React.memo`, `useMemo`, `useCallback`)

*   **`React.memo`:** Prevents a functional component from re-rendering if its props have not changed. (See question 8 for more details).
*   **`useMemo`:** Memoizes a value, preventing expensive calculations from re-running on every render. (See question 8 for more details).
*   **`useCallback`:** Memoizes a function, preventing it from being re-created on every render. This is particularly useful when passing callbacks to memoized child components.

    ```jsx
    import React, { useState, useCallback } from 'react';

    function Parent() {
      const [count, setCount] = useState(0);

      const handleClick = useCallback(() => {
        setCount(count + 1);
      }, [count]); // Only re-create if count changes

      return <Child onClick={handleClick} />;
    }

    const Child = React.memo(({ onClick }) => {
      console.log('Child rendered');
      return <button onClick={onClick}>Click me</button>;
    });
    ```

### 2. Code Splitting and Lazy Loading

Code splitting and lazy loading help reduce the initial bundle size and improve load times by loading components and code only when they are needed. (See questions 16 and 17 for more details).

### 3. Virtualization/Windowing

For long lists of data, rendering all items at once can be very slow. **Virtualization** (also known as windowing) is a technique where you only render the items that are currently visible in the viewport. Libraries like `react-window` and `react-virtualized` can help with this.

### 4. Optimizing Images

Large images can significantly slow down your page. Always optimize your images:

*   **Compress images:** Use tools to reduce file size without losing quality.
*   **Use appropriate formats:** JPEG for photos, PNG for graphics with transparency, WebP for better compression.
*   **Responsive images:** Use `srcset` and `sizes` to serve different image sizes based on the user's device.
*   **Lazy load images:** Load images only when they are about to enter the viewport.

### 5. Using the Production Build

React's development build includes extra warnings and debugging tools that are not present in the production build. Always deploy the production build of your React application for optimal performance.

### 6. Performance Monitoring

*   **React DevTools Profiler:** A powerful tool for analyzing the performance of your React components.
*   **Lighthouse:** An automated tool for improving the quality of web pages, including performance.

## Resources

*   **Article:** [React Docs - Optimizing Performance](https://reactjs.org/docs/optimizing-performance.html)
*   **Article:** [A Deep Dive into React Performance Optimization](https://www.freecodecamp.org/news/a-deep-dive-into-react-performance-optimization/)
*   **Video:** [React Performance Optimization - Academind](https://www.youtube.com/watch?v=f_g1Q0-g_1Q)
*   **Library:** [react-window](https://react-window.vercel.app/)
*   **Library:** [react-virtualized](https://bvaughn.github.io/react-virtualized/)
