
# 5. Routing Basics in Next.js

## Quick Revision

**Routing** in Next.js is primarily file-system based. This means that files and folders within the `pages` directory automatically become routes in your application. Next.js supports various routing patterns:

*   **Index routes:** `pages/index.js` maps to `/`.
*   **Nested routes:** `pages/blog/index.js` maps to `/blog`.
*   **Dynamic routes:** `pages/posts/[id].js` maps to `/posts/1`, `/posts/abc`, etc.

## Detailed Explanation

Next.js simplifies routing by abstracting away the need for a separate routing library. The file system is the API for routing.

### 1. Index Routes

*   `pages/index.js` -> `/`
*   `pages/blog/index.js` -> `/blog`

### 2. Nested Routes

Folders within the `pages` directory create nested routes.

*   `pages/dashboard/settings.js` -> `/dashboard/settings`

### 3. Dynamic Routes

To create dynamic routes, you can use square brackets (`[]`) in the file name.

*   `pages/posts/[id].js` will match paths like `/posts/1`, `/posts/abc`, etc. The `id` parameter will be available in `router.query`.

### 4. Catch-all Routes

To create catch-all routes, you can use three dots (`...`) inside square brackets.

*   `pages/posts/[...slug].js` will match `/posts/a`, `/posts/a/b`, `/posts/a/b/c`, etc. The `slug` parameter will be an array in `router.query`.

### 5. The `Link` Component

Next.js provides a `Link` component for client-side navigation between pages. Using `Link` is crucial for performance as it prefetches pages in the background.

```jsx
import Link from 'next/link';

function HomePage() {
  return (
    <ul>
      <li>
        <Link href="/">
          <a>Home</a>
        </Link>
      </li>
      <li>
        <Link href="/about">
          <a>About</a>
        </Link>
      </li>
    </ul>
  );
}
```

### 6. The `useRouter` Hook

The `useRouter` hook (from `next/router`) allows you to access the router object inside your components. You can use it to programmatically navigate, access query parameters, and more.

```jsx
import { useRouter } from 'next/router';

function MyPage() {
  const router = useRouter();

  const handleClick = () => {
    router.push('/dashboard');
  };

  return (
    <button onClick={handleClick}>Go to Dashboard</button>
  );
}
```

## Code Examples

### Dynamic Route (`pages/posts/[id].js`)

```jsx
import { useRouter } from 'next/router';

function Post() {
  const router = useRouter();
  const { id } = router.query;

  return (
    <div>
      <h1>Post: {id}</h1>
    </div>
  );
}

export default Post;
```

### Catch-all Route (`pages/docs/[...slug].js`)

```jsx
import { useRouter } from 'next/router';

function Doc() {
  const router = useRouter();
  const { slug } = router.query;

  return (
    <div>
      <h1>Docs: {slug ? slug.join('/') : ''}</h1>
    </div>
  );
}

export default Doc;
```

## Resources

*   **Article:** [Next.js Docs - Routing](https://nextjs.org/docs/routing/introduction)
*   **Article:** [Next.js Docs - `next/link`](https://nextjs.org/docs/api-reference/next/link)
*   **Article:** [Next.js Docs - `next/router`](https://nextjs.org/docs/api-reference/next/router)
*   **Video:** [Next.js Routing Tutorial - Traversy Media](https://www.youtube.com/watch?v=K7C_0_2_200)
