
# 14. Error Handling in Next.js

## Quick Revision

Effective **error handling** is crucial for building robust Next.js applications. Next.js provides several mechanisms to handle errors gracefully, both on the client-side and server-side, ensuring a better user experience and easier debugging.

Key aspects include:

*   **Custom Error Pages:** `pages/404.js` and `pages/500.js`.
*   **Error Boundaries:** For client-side React component errors.
*   **API Route Error Handling:** Using `try...catch` blocks in API routes.
*   **`_error.js`:** A special page to handle server-side errors.

## Detailed Explanation

### 1. Custom Error Pages

Next.js allows you to define custom error pages for common HTTP status codes.

*   **`pages/404.js`:** This page is rendered when a user navigates to a non-existent route. You can create a custom `404.js` file to provide a more user-friendly experience.

*   **`pages/500.js`:** This page is rendered when a server-side error occurs. It's a good practice to provide a custom `500.js` page to display a generic error message to the user, rather than exposing sensitive error details.

### 2. Error Boundaries

Error boundaries are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI. They are essential for client-side error handling within your React components.

(See React question 12 for a detailed explanation and code example of Error Boundaries).

### 3. API Route Error Handling

API Routes run on the server, so you should use standard Node.js error handling techniques, primarily `try...catch` blocks.

```javascript
// pages/api/data.js
export default async function handler(req, res) {
  try {
    // Simulate an error
    if (Math.random() > 0.5) {
      throw new Error('Failed to fetch data');
    }
    res.status(200).json({ message: 'Data fetched successfully' });
  } catch (error) {
    console.error('API Error:', error);
    res.status(500).json({ message: error.message || 'Internal Server Error' });
  }
}
```

### 4. `_error.js` (Custom Error Page for Server-Side Errors)

The `pages/_error.js` file is a special page that Next.js uses to render errors. It's primarily used for server-side errors (e.g., errors in `getServerSideProps` or API Routes) and client-side errors that are not caught by an Error Boundary.

```jsx
// pages/_error.js
import React from 'react';

function Error({ statusCode }) {
  return (
    <p>
      {statusCode
        ? `An error ${statusCode} occurred on server`
        : 'An error occurred on client'}
    </p>
  );
}

Error.getInitialProps = ({ res, err }) => {
  const statusCode = res ? res.statusCode : err ? err.statusCode : 404;
  return { statusCode };
};

export default Error;
```

## Resources

*   **Article:** [Next.js Docs - Custom Error Page](https://nextjs.org/docs/advanced-features/custom-error-page)
*   **Article:** [Next.js Docs - Error Handling](https://nextjs.org/docs/api-routes/introduction#error-handling)
*   **Article:** [React Docs - Error Boundaries](https://reactjs.org/docs/error-boundaries.html)
