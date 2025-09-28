
# 8. Dynamic Routing in Next.js

## Quick Revision

**Dynamic routing** in Next.js allows you to create pages with routes that are not fixed but depend on data. This is achieved by using square brackets (`[]`) in the file name within the `pages` directory.

For example, `pages/posts/[id].js` will match URLs like `/posts/1`, `/posts/hello-world`, etc., where `id` is a dynamic segment of the URL.

## Detailed Explanation

Next.js's file-system based router automatically handles dynamic routes. When you create a file or folder with square brackets in its name, Next.js treats the content within the brackets as a dynamic parameter.

### How Dynamic Routes Work

1.  **File Naming Convention:** Create a file like `pages/posts/[slug].js`.
2.  **Parameter Access:** The dynamic segment (`slug` in this case) will be available as a query parameter in your page component via `useRouter().query` or in data fetching functions (`getStaticProps`, `getServerSideProps`) via `context.params`.

### Catch-all Routes

For more flexible dynamic routes, you can use **catch-all routes** by adding three dots (`...`) inside the square brackets, e.g., `pages/docs/[...slug].js`.

*   This will match `/docs/a`, `/docs/a/b`, `/docs/a/b/c`, and so on.
*   The `slug` parameter will be an array containing all the segments in the URL.

### Optional Catch-all Routes

To make a catch-all route optional, you can double-bracket the parameter, e.g., `pages/[[...slug]].js`.

*   This will match `/`, `/a`, `/a/b`, etc.

## Code Examples

### Basic Dynamic Route (`pages/posts/[id].js`)

```jsx
import { useRouter } from 'next/router';

function Post() {
  const router = useRouter();
  const { id } = router.query; // 'id' will be the dynamic segment from the URL

  return (
    <div>
      <h1>Post ID: {id}</h1>
      <p>This is a dynamically routed page.</p>
    </div>
  );
}

export default Post;
```

If you navigate to `/posts/123`, `id` will be `"123"`.

### Catch-all Route (`pages/docs/[...slug].js`)

```jsx
import { useRouter } from 'next/router';

function DocPage() {
  const router = useRouter();
  const { slug } = router.query; // 'slug' will be an array

  return (
    <div>
      <h1>Documentation Page</h1>
      {slug && <p>Path: {slug.join('/')}</p>}
    </div>
  );
}

export default DocPage;
```

If you navigate to `/docs/getting-started/installation`, `slug` will be `["getting-started", "installation"]`.

### Using Dynamic Routes with Data Fetching

```jsx
// pages/products/[productId].js
import React from 'react';

function ProductDetail({ product }) {
  if (!product) return <div>Loading...</div>;
  return (
    <div>
      <h1>{product.name}</h1>
      <p>{product.description}</p>
    </div>
  );
}

export async function getServerSideProps(context) {
  const { productId } = context.params;
  const res = await fetch(`https://api.example.com/products/${productId}`);
  const product = await res.json();

  return {
    props: { product },
  };
}

export default ProductDetail;
```

## Resources

*   **Article:** [Next.js Docs - Dynamic Routes](https://nextjs.org/docs/routing/dynamic-routes)
*   **Video:** [Next.js Dynamic Routes Tutorial - Traversy Media](https://www.youtube.com/watch?v=K7C_0_2_200)
