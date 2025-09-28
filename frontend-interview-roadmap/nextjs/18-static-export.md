
# 18. Static Export in Next.js

## Quick Revision

**Static export** in Next.js allows you to export your application as a set of static HTML, CSS, and JavaScript files. This means that your application can be hosted on any static file server or CDN, without the need for a Node.js server.

This is ideal for applications that primarily use Static Site Generation (SSG) and do not require server-side rendering (SSR) or API Routes at runtime.

## Detailed Explanation

By default, Next.js applications are deployed to a Node.js server (or serverless functions on platforms like Vercel) to support features like SSR and API Routes. However, if your application is entirely static (i.e., all data is fetched at build time using `getStaticProps` and you don't use API Routes), you can export it as a static site.

### How Static Export Works

1.  **Configuration:** You need to add `output: 'export'` to your `next.config.js` file.

    ```javascript
    // next.config.js
    module.exports = {
      output: 'export',
    };
    ```

2.  **Build Command:** Run the `next build` command.

3.  **Export Command:** Run the `next export` command (or `npm run export` if configured in `package.json`). This command will generate an `out` directory containing all the static assets of your application.

### Limitations

When using static export, you lose the following Next.js features:

*   **Server-Side Rendering (SSR):** `getServerSideProps` will not work.
*   **API Routes:** API routes will not work.
*   **Image Optimization:** The `next/image` component will not perform on-demand image optimization. You'll need to pre-optimize images or use a third-party image CDN.
*   **Rewrites, Redirects, Headers:** These features, typically handled by Next.js's server, will not work. You'll need to configure them at your static hosting provider.

### When to Use Static Export

*   **Simple marketing websites:** Websites with content that rarely changes.
*   **Blogs and documentation sites:** Where content is primarily static.
*   **Hosting on traditional static hosts:** Such as GitHub Pages, Netlify, AWS S3, etc.

## Code Example

### `next.config.js`

```javascript
// next.config.js
/** @type {import('next').NextConfig} */
const nextConfig = {
  output: 'export',
  // Optional: Configure a base path if deploying to a subdirectory
  // basePath: '/my-app',
};

module.exports = nextConfig;
```

### `package.json` scripts

```json
{
  "name": "my-static-nextjs-app",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "export": "next export" // Add this script
  },
  "dependencies": {
    "next": "latest",
    "react": "latest",
    "react-dom": "latest"
  }
}
```

After running `npm run build && npm run export`, a new `out` folder will be created in your project root. This folder contains the static assets that you can deploy.

## Resources

*   **Article:** [Next.js Docs - Static HTML Export](https://nextjs.org/docs/app/api-reference/next-config-js/output#static-html-export)
*   **Video:** [Next.js Static Export - Traversy Media](https://www.youtube.com/watch?v=K7C_0_2_200)
