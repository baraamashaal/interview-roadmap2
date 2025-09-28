
# 1. CSR vs. SSR vs. SSG in Next.js

## Quick Revision

Next.js offers various rendering strategies, each with its own benefits and trade-offs for performance, SEO, and user experience.

*   **Client-Side Rendering (CSR):** The browser downloads a minimal HTML page and the JavaScript bundle, then React renders the application in the browser. Data fetching happens after the initial render.

*   **Server-Side Rendering (SSR):** The server renders the React application to an HTML string on each request and sends a fully rendered HTML page to the browser. React then "hydrates" this HTML on the client.

*   **Static Site Generation (SSG):** The HTML is generated at build time and reused for each request. This is ideal for content that doesn't change frequently.

## Detailed Explanation

### Client-Side Rendering (CSR)

This is the default rendering method for traditional Single-Page Applications (SPAs) built with React without a framework like Next.js.

**Process:**

1.  The browser requests an HTML file.
2.  The server sends a minimal HTML file (often just a `<div id="root"></div>`) and a link to the JavaScript bundle.
3.  The browser downloads the JavaScript bundle.
4.  The JavaScript executes, fetches data (if any), and renders the UI into the DOM.

**Pros:**

*   Fast initial page load (minimal HTML).
*   Rich, interactive user experience after initial load.

**Cons:**

*   Poor SEO (search engines might struggle to crawl content rendered by JavaScript).
*   Slower Time To Interactive (TTI) as users wait for JavaScript to load and execute.

### Server-Side Rendering (SSR)

SSR generates the full HTML for a page on the server for each request. Next.js provides `getServerSideProps` for this.

**Process:**

1.  The browser requests a page.
2.  The server fetches data (if needed) and renders the React component into an HTML string.
3.  The server sends the fully formed HTML to the browser.
4.  The browser displays the HTML. The user sees content immediately.
5.  The browser downloads the JavaScript bundle.
6.  React "hydrates" the HTML, making the page interactive.

**Pros:**

*   Good for SEO (full HTML available to crawlers).
*   Faster First Contentful Paint (FCP) and Time To Interactive (TTI) compared to CSR.
*   Always up-to-date data on each request.

**Cons:**

*   Slower Time To First Byte (TTFB) due to server rendering on each request.
*   Increased server load.

### Static Site Generation (SSG)

SSG generates the HTML for a page at build time. Next.js provides `getStaticProps` for this.

**Process:**

1.  At build time, Next.js fetches data (if needed) and renders the React component into an HTML string.
2.  The HTML, CSS, and JavaScript are saved as static files.
3.  When a user requests the page, the CDN serves the pre-built HTML directly.
4.  The browser displays the HTML immediately.
5.  The browser downloads the JavaScript bundle.
6.  React "hydrates" the HTML, making the page interactive.

**Pros:**

*   Extremely fast page loads (served from CDN).
*   Excellent for SEO.
*   Reduced server load (no server rendering on request).
*   Highly scalable and secure.

**Cons:**

*   Data is not always up-to-date (requires a re-build for content changes).
*   Not suitable for pages with frequently changing, user-specific data.

## When to Use Which

*   **CSR:** For dashboards, admin panels, or applications where SEO is not critical and data is highly dynamic.
*   **SSR:** For pages with dynamic, user-specific data that needs to be fresh on every request (e.g., e-commerce product pages, user profiles).
*   **SSG:** For marketing pages, blogs, documentation, or any content that doesn't change frequently and can be pre-rendered.

## Resources

*   **Article:** [Next.js Docs - Data Fetching](https://nextjs.org/docs/basic-features/data-fetching)
*   **Article:** [Next.js Docs - Rendering](https://nextjs.org/docs/advanced-features/rendering)
*   **Video:** [Next.js Rendering Strategies Explained - Fireship](https://www.youtube.com/watch?v=9Q_J0_0200Q)
