
# 12. Deployment Basics in Next.js

## Quick Revision

Deploying a Next.js application involves building the project and then serving the optimized output. Next.js applications can be deployed to various platforms, including serverless functions, Node.js servers, or static hosting services.

*   **`next build`:** Compiles your application for production.
*   **`next start`:** Starts a Next.js production server.
*   **Vercel:** The recommended platform for deploying Next.js applications, offering zero-configuration deployment.

## Detailed Explanation

Next.js applications are highly flexible in terms of deployment targets due to their pre-rendering capabilities (SSG and SSR).

### 1. Build Process

To prepare your Next.js application for deployment, you first need to build it:

```bash
npm run build
# or
yarn build
```

This command runs `next build`, which:

*   Creates an optimized production build of your application.
*   Generates HTML, CSS, and JavaScript files.
*   Optimizes images, fonts, and other assets.
*   Outputs the build artifacts to the `.next` folder.

### 2. Serving the Application

#### a. Vercel (Recommended)

Vercel is the creator of Next.js and provides a seamless, zero-configuration deployment experience. It automatically detects Next.js projects and deploys them with optimal settings.

**Deployment Steps:**

1.  Install the Vercel CLI: `npm i -g vercel`
2.  Navigate to your project directory.
3.  Run `vercel`.

Vercel automatically handles:

*   Building your project.
*   Deploying static assets to a CDN.
*   Deploying server-side rendered pages and API routes as serverless functions.
*   Setting up custom domains and HTTPS.

#### b. Node.js Server

You can deploy your Next.js application to a custom Node.js server. This is useful if you need more control over the server environment or if you are deploying to a platform that doesn't support serverless functions.

**Deployment Steps:**

1.  Build your project: `npm run build`
2.  Start the production server: `npm run start` (which runs `next start`)

This will start a Node.js server that serves your Next.js application.

#### c. Static Hosting (for SSG-only applications)

If your Next.js application only uses Static Site Generation (SSG) and does not have any `getServerSideProps` or API Routes, you can export it as a static HTML application.

**Deployment Steps:**

1.  Modify `next.config.js`:

    ```javascript
    // next.config.js
    module.exports = {
      output: 'export',
    };
    ```

2.  Build your project: `npm run build`
3.  Export the static files: `npm run export` (which runs `next export`)

This will generate a `out` folder containing static HTML, CSS, and JavaScript files that can be deployed to any static hosting service (e.g., GitHub Pages, Netlify, AWS S3).

## Resources

*   **Article:** [Next.js Docs - Deployment](https://nextjs.org/docs/deployment)
*   **Platform:** [Vercel](https://vercel.com/)
*   **Video:** [Deploying Next.js to Vercel - Traversy Media](https://www.youtube.com/watch?v=K7C_0_2_200)
