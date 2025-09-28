
# 2. `getStaticProps` vs. `getServerSideProps` in Next.js

## Quick Revision

Next.js provides two primary functions for data fetching in server-side environments:

*   **`getStaticProps` (Static Site Generation - SSG):** Fetches data at **build time**. The data is pre-rendered into HTML and reused for every request. Ideal for data that doesn't change frequently.

*   **`getServerSideProps` (Server-Side Rendering - SSR):** Fetches data on **each request**. The data is pre-rendered into HTML on the server for every incoming request. Ideal for data that changes frequently or is user-specific.

## Detailed Explanation

Both `getStaticProps` and `getServerSideProps` are asynchronous functions that run only on the server-side. They are used to fetch data and pass it as props to your React components.

### `getStaticProps`

*   **Execution:** Runs at **build time**. This means the data is fetched once when you build your Next.js application, and the resulting HTML is cached and served for all subsequent requests.
*   **When to use:**
    *   Data that is publicly available and doesn't change often (e.g., blog posts, product listings).
    *   When SEO is critical, as the full HTML is available at build time.
    *   When you want the fastest possible page load times (served from a CDN).
*   **Revalidation:** Can be revalidated using Incremental Static Regeneration (ISR) to update static pages after they have been built.

### `getServerSideProps`

*   **Execution:** Runs on **each request**. This means that for every incoming request to a page, Next.js will execute `getServerSideProps` on the server, fetch the data, and then render the page.
*   **When to use:**
    *   Data that changes frequently and needs to be up-to-date on every request (e.g., real-time stock prices, user-specific dashboards).
    *   When the data is user-specific and cannot be pre-rendered.
*   **Performance:** Can be slower than SSG because the server has to fetch data and render the page on every request.

## Code Examples

### `getStaticProps` Example

```jsx
// pages/blog/[slug].js
import React from 'react';

function BlogPost({ post }) {
  return (
    <div>
      <h1>{post.title}</h1>
      <p>{post.content}</p>
    </div>
  );
}

export async function getStaticProps(context) {
  // Fetch data from an API or database at build time
  const res = await fetch(`https://api.example.com/posts/${context.params.slug}`);
  const post = await res.json();

  return {
    props: { post },
    revalidate: 60, // Revalidate every 60 seconds (ISR)
  };
}

export async function getStaticPaths() {
  // Fetch all possible paths for dynamic routes
  const res = await fetch('https://api.example.com/posts');
  const posts = await res.json();

  const paths = posts.map((post) => ({
    params: { slug: post.slug },
  }));

  return { paths, fallback: 'blocking' };
}

export default BlogPost;
```

### `getServerSideProps` Example

```jsx
// pages/dashboard.js
import React from 'react';

function Dashboard({ user }) {
  return (
    <div>
      <h1>Welcome, {user.name}</h1>
      <p>Your email: {user.email}</p>
    </div>
  );
}

export async function getServerSideProps(context) {
  // Fetch user-specific data on each request
  const res = await fetch(`https://api.example.com/users/${context.req.cookies.userId}`);
  const user = await res.json();

  if (!user) {
    return {
      notFound: true,
    };
  }

  return {
    props: { user },
  };
}

export default Dashboard;
```

## Summary

| Feature      | `getStaticProps` (SSG)                   | `getServerSideProps` (SSR)               |
|--------------|------------------------------------------|------------------------------------------|
| **Execution**| Build time                               | Each request                             |
| **Data Freshness**| Stale (can be revalidated with ISR)      | Always up-to-date                        |
| **SEO**      | Excellent                                | Excellent                                |
| **Performance**| Very fast (served from CDN)              | Slower (server rendering on request)     |
| **Use Case** | Static content, blogs, marketing pages   | Dynamic, user-specific data              |

## Resources

*   **Article:** [Next.js Docs - `getStaticProps`](https://nextjs.org/docs/basic-features/data-fetching/get-static-props)
*   **Article:** [Next.js Docs - `getServerSideProps`](https://nextjs.org/docs/basic-features/data-fetching/get-server-side-props)
*   **Video:** [Next.js Data Fetching Explained - Fireship](https://www.youtube.com/watch?v=9Q_J0_0200Q)
