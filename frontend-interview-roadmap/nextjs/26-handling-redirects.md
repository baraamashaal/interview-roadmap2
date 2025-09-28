
# 26. Handling Redirects in Next.js

## Quick Revision

**Redirects** are used to send users and search engines from one URL to another. Next.js provides several ways to handle redirects, both permanent (301) and temporary (307/308), to manage URL changes, maintain SEO, and improve user experience.

Key methods include:

*   **`next.config.js` redirects:** For static, persistent redirects.
*   **`getServerSideProps` redirects:** For dynamic, server-side redirects.
*   **`next/router` redirects:** For client-side redirects.
*   **Middleware redirects:** For powerful, programmatic redirects before a request is completed.

## Detailed Explanation

Redirects are essential for maintaining a healthy website, especially when URLs change or content moves. Next.js offers flexible options to implement them.

### 1. `next.config.js` Redirects

This is the recommended way to handle static redirects that don't change frequently. These redirects are processed at build time and are very performant.

```javascript
// next.config.js
module.exports = {
  async redirects() {
    return [
      {
        source: '/old-page',
        destination: '/new-page',
        permanent: true, // 301 redirect
      },
      {
        source: '/beta',
        destination: '/dashboard',
        permanent: false, // 307 redirect
      },
    ];
  },
};
```

*   **`permanent: true`:** Sends a 301 (Moved Permanently) status code, which is good for SEO as it tells search engines that the content has permanently moved.
*   **`permanent: false`:** Sends a 307 (Temporary Redirect) status code, indicating a temporary move.

### 2. `getServerSideProps` Redirects

For dynamic redirects that depend on data or user authentication, you can use `getServerSideProps`.

```jsx
// pages/protected-page.js
export async function getServerSideProps(context) {
  const isAuthenticated = /* check authentication logic */ false;

  if (!isAuthenticated) {
    return {
      redirect: {
        destination: '/login',
        permanent: false,
      },
    };
  }

  return {
    props: {},
  };
}
```

### 3. `next/router` Client-Side Redirects

You can use the `useRouter` hook for client-side redirects, typically after a user action (e.g., form submission).

```jsx
import { useRouter } from 'next/router';

function MyComponent() {
  const router = useRouter();

  const handleClick = () => {
    // Perform some action
    router.push('/dashboard'); // Client-side navigation
  };

  return <button onClick={handleClick}>Go to Dashboard</button>;
}
```

### 4. Middleware Redirects

Next.js Middleware provides a powerful way to handle redirects programmatically before a request is completed. This is useful for global redirects, A/B testing, or advanced authentication flows.

```javascript
// middleware.js
import { NextResponse } from 'next/server';

export function middleware(request) {
  if (request.nextUrl.pathname === '/old-route') {
    return NextResponse.redirect(new URL('/new-route', request.url));
  }
  return NextResponse.next();
}
```

## Resources

*   **Article:** [Next.js Docs - Redirects](https://nextjs.org/docs/api-reference/next.config.js/redirects)
*   **Article:** [Next.js Docs - `getServerSideProps` Redirects](https://nextjs.org/docs/basic-features/data-fetching/get-server-side-props#redirect)
*   **Article:** [Next.js Docs - `next/router` Redirects](https://nextjs.org/docs/api-reference/next/router#routerpushhref-as-options)
*   **Article:** [Next.js Docs - Middleware Redirects](https://nextjs.org/docs/advanced-features/middleware#redirecting)
