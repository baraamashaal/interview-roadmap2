
# 27. `getInitialProps` in Next.js

## Quick Revision

**`getInitialProps`** is a legacy data fetching method in Next.js that was used to fetch data for a page on both the server-side and client-side. It has largely been superseded by `getStaticProps` and `getServerSideProps` for better performance and clearer data fetching strategies.

## Detailed Explanation

`getInitialProps` was the original data fetching method in Next.js. It allowed you to fetch data for a page before it was rendered, regardless of whether the page was being rendered on the server or the client.

### How `getInitialProps` Worked

*   **Server-side:** If the page was requested directly (e.g., by typing the URL in the browser), `getInitialProps` would run on the server.
*   **Client-side:** If the page was navigated to via `next/link` or `router.push`, `getInitialProps` would run on the client.

### The `context` Object

`getInitialProps` received a `context` object with the following properties:

*   `pathname`: The path of the page.
*   `query`: The query string parsed as an object.
*   `asPath`: The actual path (including the query) shown in the browser.
*   `req`: The HTTP request object (server-side only).
*   `res`: The HTTP response object (server-side only).
*   `err`: Error object if any error was encountered during rendering.

### Why it's Deprecated (or less recommended)

`getInitialProps` has been largely replaced by `getStaticProps` and `getServerSideProps` because:

*   **Lack of clarity:** It was often unclear whether `getInitialProps` would run on the server or client, leading to potential issues.
*   **Performance:** It didn't allow for the same level of optimization as `getStaticProps` (build-time generation) or `getServerSideProps` (per-request server rendering).
*   **Bundle size:** It would often include server-side code in the client-side bundle.

## Code Example

```jsx
import React from 'react';

function MyPage({ stars }) {
  return (
    <div>
      <h1>Next stars: {stars}</h1>
    </div>
  );
}

MyPage.getInitialProps = async (context) => {
  const res = await fetch('https://api.github.com/repos/vercel/next.js');
  const json = await res.json();
  return { stars: json.stargazers_count };
};

export default MyPage;
```

## When to Use `getInitialProps` (Rarely)

While `getInitialProps` is generally discouraged for new projects, there are a few niche cases where it might still be used:

*   **Custom `_app.js`:** If you need to fetch data that is common to all pages in your application, you can use `getInitialProps` in `pages/_app.js`.
*   **Legacy projects:** For maintaining older Next.js applications.

For most data fetching needs, `getStaticProps` and `getServerSideProps` are the preferred methods.

## Resources

*   **Article:** [Next.js Docs - `getInitialProps`](https://nextjs.org/docs/api-reference/data-fetching/get-initial-props)
*   **Article:** [Next.js Data Fetching: `getStaticProps`, `getServerSideProps`, and `getInitialProps`](https://www.freecodecamp.org/news/nextjs-data-fetching-getstaticprops-getserversideprops-getinitialprops/)
