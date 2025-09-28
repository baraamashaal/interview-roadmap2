
# 9. Middleware in Next.js

## Quick Revision

**Next.js Middleware** allows you to run code before a request is completed. It acts as a bridge between the incoming request and the page or API route that handles it. Middleware can be used for a variety of tasks, such as:

*   **Authentication:** Protecting routes by checking user authentication.
*   **Authorization:** Checking user permissions.
*   **Rewriting/Redirecting:** Modifying the incoming request or redirecting to a different URL.
*   **A/B Testing:** Implementing A/B testing by modifying headers or cookies.
*   **Internationalization:** Handling locale detection and redirection.

## Detailed Explanation

Middleware functions are defined in a `middleware.js` (or `middleware.ts`) file at the root of your project (or within `src/`). They run on the Edge Runtime, which is a fast, lightweight runtime environment.

### How Middleware Works

1.  A request comes into your Next.js application.
2.  The middleware function is executed **before** any page or API route handler.
3.  The middleware can then:
    *   **Rewrite** the request to a different URL.
    *   **Redirect** the user to a different URL.
    *   **Modify** request or response headers/cookies.
    *   **Return a response** directly, short-circuiting the request.

### `NextRequest` and `NextResponse`

Next.js provides `NextRequest` and `NextResponse` objects for working with requests and responses in middleware. These are extensions of the standard Web `Request` and `Response` APIs.

## Code Examples

### Basic Authentication Middleware

Create a file `middleware.js` at the root of your project:

```javascript
// middleware.js
import { NextResponse } from 'next/server';

export function middleware(request) {
  const isAuthenticated = /* logic to check if user is authenticated */ true;

  if (!isAuthenticated && request.nextUrl.pathname.startsWith('/dashboard')) {
    return NextResponse.redirect(new URL('/login', request.url));
  }

  return NextResponse.next();
}

// Optionally, define a matcher to run middleware only on specific paths
export const config = {
  matcher: ['/dashboard/:path*'],
};
```

In this example, if a user tries to access any path under `/dashboard` and is not authenticated, they will be redirected to the `/login` page.

### Rewriting a Request

```javascript
// middleware.js
import { NextResponse } from 'next/server';

export function middleware(request) {
  if (request.nextUrl.pathname.startsWith('/old-path')) {
    return NextResponse.rewrite(new URL('/new-path', request.url));
  }
  return NextResponse.next();
}
```

This middleware rewrites requests from `/old-path` to `/new-path` internally, so the user's URL in the browser remains `/old-path`.

### Setting Headers

```javascript
// middleware.js
import { NextResponse } from 'next/server';

export function middleware(request) {
  const response = NextResponse.next();
  response.headers.set('x-custom-header', 'Hello from Middleware');
  return response;
}
```

## Resources

*   **Article:** [Next.js Docs - Middleware](https://nextjs.org/docs/advanced-features/middleware)
*   **Video:** [Next.js Middleware Tutorial - Traversy Media](https://www.youtube.com/watch?v=K7C_0_2_200)
