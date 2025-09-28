
# 24. ISR Revalidation in Next.js

## Quick Revision

**ISR (Incremental Static Regeneration) revalidation** is the mechanism by which Next.js updates statically generated pages after they have been deployed. It allows you to serve stale content immediately while new content is generated in the background, combining the benefits of static sites (speed, SEO) with dynamic content updates.

Revalidation is configured using the `revalidate` property within `getStaticProps`.

## Detailed Explanation

Static Site Generation (SSG) is great for performance and SEO because pages are pre-built at compile time. However, a limitation of traditional SSG is that content updates require a full rebuild and redeployment of the site.

ISR addresses this by allowing you to specify a time-based revalidation period for your static pages. When a page is requested:

1.  **Initial Request:** The pre-built static page is served immediately from the cache (e.g., CDN).
2.  **Revalidation Trigger:** If the time since the last page generation exceeds the `revalidate` duration, Next.js serves the **stale** (cached) page to the user.
3.  **Background Regeneration:** In the background, Next.js initiates a new server-side render for that page, fetching the latest data.
4.  **Cache Update:** Once the new page is successfully generated, it replaces the stale page in the cache.
5.  **Subsequent Requests:** Future requests will receive the newly generated, fresh page.

This ensures that users always get a fast response, and the content eventually becomes up-to-date.

### How to Configure `revalidate`

The `revalidate` property is set in seconds within the object returned by `getStaticProps`.

```javascript
export async function getStaticProps() {
  // Fetch data
  const data = await fetchData();

  return {
    props: { data },
    revalidate: 60, // Page will be re-generated at most once every 60 seconds
  };
}
```

### On-Demand Revalidation

Next.js also supports **on-demand revalidation**, which allows you to programmatically purge the cache for a specific page (or path) when content changes (e.g., after a CMS update). This is done by calling a special API route from your CMS webhook.

```javascript
// pages/api/revalidate.js
export default async function handler(req, res) {
  // Check for secret to confirm this is a valid request
  if (req.query.secret !== process.env.MY_SECRET_TOKEN) {
    return res.status(401).json({ message: 'Invalid token' });
  }

  try {
    // Revalidate a specific path
    await res.revalidate('/blog/post-1');
    return res.json({ revalidated: true });
  } catch (err) {
    // If there was an error, Next.js will continue to serve the last successfully generated page
    return res.status(500).send('Error revalidating');
  }
}
```

## Benefits of ISR Revalidation

*   **Always Fresh Content:** Content can be updated without a full site rebuild.
*   **Fast Page Loads:** Initial page loads are still served from static files.
*   **Improved SEO:** Search engines always get up-to-date content.
*   **Reduced Build Times:** Only affected pages are re-generated, not the entire site.

## Resources

*   **Article:** [Next.js Docs - Incremental Static Regeneration](https://nextjs.org/docs/basic-features/data-fetching/incremental-static-regeneration)
*   **Article:** [Next.js Docs - On-demand Revalidation](https://nextjs.org/docs/basic-features/data-fetching/incremental-static-regeneration#on-demand-revalidation)
*   **Video:** [Next.js ISR Explained - Fireship](https://www.youtube.com/watch?v=N5R6oX6bLpA)
