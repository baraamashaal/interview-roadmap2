
# 13. Authentication in Next.js

## Quick Revision

**Authentication** in Next.js involves verifying a user's identity and managing their session. Due to Next.js's hybrid rendering capabilities (CSR, SSR, SSG), authentication strategies can vary. Common approaches include:

*   **Session-based authentication:** Using cookies to store session IDs.
*   **Token-based authentication:** Using JWTs (JSON Web Tokens) for stateless authentication.
*   **Third-party authentication:** Integrating with providers like Google, GitHub, etc., often via libraries like NextAuth.js.

## Detailed Explanation

Authentication in Next.js needs to consider both client-side and server-side contexts.

### 1. Session-Based Authentication

*   **How it works:** When a user logs in, the server creates a session and stores a session ID in a cookie on the client. On subsequent requests, the server verifies the session ID.
*   **Pros:** Simple to implement for traditional web apps.
*   **Cons:** Requires a server to manage sessions, not ideal for highly scalable or distributed systems.

### 2. Token-Based Authentication (JWT)

*   **How it works:** When a user logs in, the server issues a JWT. The client stores this token (e.g., in `localStorage` or an HTTP-only cookie) and sends it with every request. The server verifies the token's authenticity.
*   **Pros:** Stateless, scalable, can be used across multiple services.
*   **Cons:** Requires careful handling of token storage (especially XSS risks with `localStorage`).

### 3. Third-Party Authentication (OAuth, OpenID Connect)

*   **How it works:** Users authenticate through a third-party provider (e.g., Google, GitHub). The provider returns an access token, which your application uses to access user data.
*   **Pros:** Convenient for users, offloads authentication complexity to trusted providers.
*   **Cons:** Adds external dependency.

### Next.js Specifics

*   **API Routes:** Ideal for handling authentication logic (login, logout, token refresh) on the server-side, keeping sensitive credentials secure.
*   **`getServerSideProps`:** Can be used to check authentication status on the server before rendering a page, protecting routes.
*   **Middleware:** Next.js Middleware (introduced in Next.js 12) is a powerful way to protect routes and redirect unauthenticated users before a page even starts rendering.

### NextAuth.js

**NextAuth.js** is a complete open-source authentication solution for Next.js applications. It supports various authentication providers (Google, GitHub, etc.), email/password, and JWTs, simplifying the implementation of secure authentication.

## Code Example (Conceptual with NextAuth.js)

### `pages/api/auth/[...nextauth].js`

```javascript
import NextAuth from 'next-auth';
import Providers from 'next-auth/providers';

export default NextAuth({
  providers: [
    Providers.GitHub({
      clientId: process.env.GITHUB_ID,
      clientSecret: process.env.GITHUB_SECRET,
    }),
    // Add other providers as needed
  ],
  // Optional: Add database, callbacks, etc.
});
```

### Protecting a Page with `getServerSideProps`

```jsx
import { getSession } from 'next-auth/client';

function ProtectedPage({ session }) {
  if (!session) {
    return <p>Access Denied</p>;
  }
  return <p>Welcome, {session.user.name}</p>;
}

export async function getServerSideProps(context) {
  const session = await getSession(context);

  if (!session) {
    return {
      redirect: {
        destination: '/api/auth/signin',
        permanent: false,
      },
    };
  }

  return {
    props: { session },
  };
}

export default ProtectedPage;
```

### Protecting a Page with Middleware

```javascript
// middleware.js
import { getToken } from 'next-auth/jwt';
import { NextResponse } from 'next/server';

export async function middleware(req) {
  const token = await getToken({ req, secret: process.env.NEXTAUTH_SECRET });

  const { pathname } = req.nextUrl;

  if (pathname.startsWith('/protected') && !token) {
    const url = new URL('/api/auth/signin', req.url);
    url.searchParams.set('callbackUrl', pathname);
    return NextResponse.redirect(url);
  }

  return NextResponse.next();
}

export const config = {
  matcher: ['/protected/:path*'],
};
```

## Resources

*   **Article:** [Next.js Docs - Authentication](https://nextjs.org/docs/authentication)
*   **Library:** [NextAuth.js](https://next-auth.js.org/)
*   **Video:** [Next.js Authentication with NextAuth.js - Traversy Media](https://www.youtube.com/watch?v=K7C_0_2_200)
