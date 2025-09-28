
# 28. Edge Functions in Next.js

## Quick Revision

**Edge Functions** (also known as Edge Middleware) in Next.js allow you to run code at the edge of the network, closer to your users. This provides extremely low latency and high performance for certain operations. They are built on Web standards (like the Request and Response APIs) and run in a lightweight JavaScript runtime (like V8).

## Detailed Explanation

Traditional serverless functions run in a specific region, which can introduce latency for users far away from that region. Edge Functions solve this by deploying your code globally to a network of edge servers.

### How Edge Functions Work

1.  **Global Deployment:** Your Edge Function code is deployed to a CDN (Content Delivery Network) of edge servers around the world.
2.  **Request Interception:** When a user makes a request, the Edge Function intercepts it at the nearest edge server.
3.  **Execution:** The Edge Function executes its logic (e.g., rewriting URLs, modifying headers, authenticating users) before the request even reaches your origin server.
4.  **Response:** The Edge Function can then return a response directly or modify the request and forward it to your origin server.

### Key Characteristics

*   **Low Latency:** Code runs geographically closer to the user.
*   **Fast Execution:** Lightweight runtime environment for quick execution.
*   **Web Standards:** Built on standard Web APIs (`Request`, `Response`, `URL`).
*   **Limited APIs:** Due to their lightweight nature, Edge Functions have a limited set of available Node.js APIs.

### Use Cases

*   **A/B Testing:** Dynamically rewrite pages or set cookies for A/B tests.
*   **Authentication/Authorization:** Protect routes and redirect unauthenticated users.
*   **Geo-targeting:** Serve different content or redirect users based on their location.
*   **URL Rewriting/Redirects:** Perform advanced URL manipulations.
*   **Bot Detection:** Identify and block malicious bots.

## Code Example

Edge Functions are typically implemented as Next.js Middleware.

```javascript
// middleware.js
import { NextResponse } from 'next/server';

export function middleware(request) {
  // Example: A/B testing based on a cookie
  const abTestCookie = request.cookies.get('ab-test');

  if (!abTestCookie) {
    const randomValue = Math.random();
    const variant = randomValue < 0.5 ? 'A' : 'B';
    const response = NextResponse.next();
    response.cookies.set('ab-test', variant);

    if (variant === 'B') {
      // Rewrite to a different page for variant B
      return NextResponse.rewrite(new URL('/variant-b', request.url));
    }
    return response;
  }

  return NextResponse.next();
}

export const config = {
  matcher: ['/'], // Run middleware on the homepage
};
```

## Resources

*   **Article:** [Next.js Docs - Middleware](https://nextjs.org/docs/advanced-features/middleware)
*   **Article:** [Vercel - Edge Functions](https://vercel.com/docs/concepts/functions/edge-functions)
*   **Video:** [Next.js Edge Functions Explained - Fireship](https://www.youtube.com/watch?v=N5R6oX6bLpA)
