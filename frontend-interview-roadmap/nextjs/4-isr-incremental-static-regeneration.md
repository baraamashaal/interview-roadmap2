
# 4. ISR (Incremental Static Regeneration) in Next.js

## Quick Revision

**Incremental Static Regeneration (ISR)** is a Next.js feature that allows you to update static pages **after** they have been built and deployed, without requiring a full site rebuild. It combines the benefits of Static Site Generation (SSG) (fast page loads, good SEO) with the ability to display fresh data.

## Detailed Explanation

With traditional SSG, pages are generated at build time. If your content changes, you need to rebuild and redeploy your entire site to see the updates. This can be slow and inefficient for sites with frequently changing content.

ISR solves this problem by allowing you to specify a `revalidate` time for your static pages. When a request comes in for a page that is older than the `revalidate` time, Next.js will:

1.  Serve the **stale (cached)** page immediately.
2.  In the background, re-generate the page with fresh data.
3.  Replace the stale page in the cache with the newly generated page.

This means users always get a fast response, and the content is eventually updated.

### How to Implement ISR

To use ISR, you need to include the `revalidate` property in the object returned by `getStaticProps`.

```javascript
export async function getStaticProps() {
  const res = await fetch('https://api.example.com/posts');
  const posts = await res.json();

  return {
    props: {
      posts,
    },
    revalidate: 60, // In seconds
  };
}
```

In this example, the page will be re-generated at most once every 60 seconds. If a request comes in after 60 seconds, the stale page will be served, and a new page will be generated in the background.

### `fallback` Property in `getStaticPaths`

When using ISR with dynamic routes, you also need to consider the `fallback` property in `getStaticPaths`:

*   **`fallback: false`:** Any path not returned by `getStaticPaths` will result in a 404 page. No new pages will be generated at runtime.
*   **`fallback: true`:** Next.js will serve a fallback version of the page (e.g., a loading spinner) for paths not returned by `getStaticPaths`. In the background, Next.js will generate the new page and then replace the fallback with the full page. This is useful for a large number of static pages.
*   **`fallback: 'blocking'`:** Next.js will block the request until the new page is generated. This means the user will not see a fallback, but they will have to wait for the page to be generated.

## Benefits of ISR

*   **Fast Page Loads:** Pages are served from a CDN, providing instant loading.
*   **Good SEO:** Fully rendered HTML is available to search engine crawlers.
*   **Fresh Content:** Content can be updated without requiring a full site rebuild.
*   **Scalability:** Reduces the load on your server by serving cached pages.

## Code Example

```jsx
// pages/products/[id].js
import React from 'react
';

function ProductPage({ product }) {
  return (
    <div>
      <h1>{product.name}</h1>
      <p>{product.description}</p>
      <p>Price: ${product.price}</p>
    </div>
  );
}

export async function getStaticPaths() {
  const res = await fetch('https://api.example.com/products');
  const products = await res.json();

  const paths = products.map((product) => ({
    params: { id: product.id.toString() },
  }));

  return { paths, fallback: 'blocking' };
}

export async function getStaticProps({ params }) {
  const res = await fetch(`https://api.example.com/products/${params.id}`);
  const product = await res.json();

  if (!product) {
    return {
      notFound: true,
    };
  }

  return {
    props: { product },
    revalidate: 10, // Re-generate the page every 10 seconds
  };
}

export default ProductPage;
```

## Resources

*   **Article:** [Next.js Docs - Incremental Static Regeneration](https://nextjs.org/docs/basic-features/data-fetching/incremental-static-regeneration)
*   **Video:** [Incremental Static Regeneration (ISR) in Next.js - Fireship](https://www.youtube.com/watch?v=N5R6oX6bLpA)
