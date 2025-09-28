
# 22. CMS Integrations in Next.js

## Quick Revision

**CMS (Content Management System) integrations** in Next.js involve connecting your Next.js frontend to a backend system that manages your content. This allows content editors to update website content without developer intervention. Next.js is particularly well-suited for this due to its pre-rendering capabilities (SSG and SSR).

Common types of CMS include:

*   **Headless CMS:** A backend-only CMS that provides content via an API (e.g., Strapi, Contentful, Sanity).
*   **Traditional CMS:** A monolithic CMS that handles both content management and frontend rendering (less common with Next.js).

## Detailed Explanation

Next.js's data fetching methods (`getStaticProps`, `getServerSideProps`) make it very flexible for integrating with various CMS solutions. The choice of CMS often depends on the project's requirements, team expertise, and content structure.

### Headless CMS

A headless CMS is a backend content management system that provides content as data (e.g., JSON) through an API (REST or GraphQL). Your Next.js application then fetches this data and renders it.

**Benefits of Headless CMS with Next.js:**

*   **Decoupled architecture:** Separates the frontend from the backend, allowing for greater flexibility.
*   **Developer experience:** Developers can use their preferred frontend technologies.
*   **Scalability:** Content can be served from a CDN, improving performance.
*   **Content reuse:** Content can be used across multiple platforms (web, mobile, etc.).

**Popular Headless CMS:**

*   **Strapi:** Open-source, self-hostable, and highly customizable.
*   **Contentful:** Cloud-based, enterprise-grade headless CMS.
*   **Sanity:** Real-time content platform with a flexible content model.

### Integration Strategies

1.  **Static Site Generation (SSG) with `getStaticProps`:**
    *   Ideal for content that doesn't change frequently (e.g., blog posts, marketing pages).
    *   Content is fetched at build time, resulting in fast, pre-rendered HTML.
    *   Can be combined with ISR (`revalidate`) to update content without a full rebuild.

2.  **Server-Side Rendering (SSR) with `getServerSideProps`:**
    *   Ideal for dynamic content that needs to be fresh on every request (e.g., user-specific dashboards).
    *   Content is fetched on the server for each request.

3.  **Client-Side Rendering (CSR):**
    *   Content is fetched directly from the client after the page has loaded.
    *   Suitable for highly interactive, user-specific content that doesn't require SEO.

## Code Example (SSG with a Headless CMS)

Let's assume you have a headless CMS that exposes a REST API for blog posts.

```jsx
// pages/blog/[slug].js
import React from 'react';

function BlogPost({ post }) {
  return (
    <div>
      <h1>{post.title}</h1>
      <div dangerouslySetInnerHTML={{ __html: post.content }} />
    </div>
  );
}

export async function getStaticPaths() {
  // Fetch all possible post slugs from your CMS
  const res = await fetch('https://your-cms.com/api/posts');
  const posts = await res.json();

  const paths = posts.map((post) => ({
    params: { slug: post.slug },
  }));

  return { paths, fallback: 'blocking' };
}

export async function getStaticProps({ params }) {
  // Fetch individual post data from your CMS
  const res = await fetch(`https://your-cms.com/api/posts/${params.slug}`);
  const post = await res.json();

  if (!post) {
    return {
      notFound: true,
    };
  }

  return {
    props: { post },
    revalidate: 60, // Revalidate every 60 seconds (ISR)
  };
}

export default BlogPost;
```

## Resources

*   **Article:** [Next.js Docs - Data Fetching](https://nextjs.org/docs/basic-features/data-fetching)
*   **Article:** [Headless CMS Explained](https://www.contentful.com/r/knowledge-base/what-is-headless-cms/)
*   **CMS:** [Strapi](https://strapi.io/)
*   **CMS:** [Contentful](https://www.contentful.com/)
*   **CMS:** [Sanity](https://www.sanity.io/)
