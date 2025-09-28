
# 17. Environment Variables in Next.js

## Quick Revision

**Environment variables** allow you to customize the behavior of your application based on the environment it's running in (e.g., development, production, test). Next.js has built-in support for environment variables, allowing you to expose them to both the server-side and client-side code.

*   **`NEXT_PUBLIC_` prefix:** Variables prefixed with `NEXT_PUBLIC_` are exposed to the browser.
*   **No prefix:** Variables without the prefix are only available on the server-side.

## Detailed Explanation

Environment variables are crucial for managing sensitive information (like API keys) and configuring different settings for various deployment environments. Next.js provides a secure and convenient way to handle them.

### How Next.js Handles Environment Variables

1.  **`.env` files:** Next.js automatically loads environment variables from `.env` files in your project root.
    *   `.env.local`: Local overrides. Not committed to Git.
    *   `.env.development`: Development environment variables.
    *   `.env.production`: Production environment variables.
    *   `.env`: Default environment variables.

2.  **Server-side only variables:** Any variable defined in your `.env` files (or system environment) without the `NEXT_PUBLIC_` prefix will only be available on the server-side (e.g., in `getStaticProps`, `getServerSideProps`, API Routes).

3.  **Client-side variables:** To expose an environment variable to the browser, you must prefix it with `NEXT_PUBLIC_`.

### Security Considerations

*   **Never expose sensitive keys to the client:** Do not prefix sensitive API keys (e.g., database credentials, secret keys) with `NEXT_PUBLIC_`. These should only be used on the server-side.
*   **Use `.env.local` for local secrets:** This file should not be committed to your version control system.

## Code Examples

### `.env.local` file

```
# .env.local
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=password

NEXT_PUBLIC_ANALYTICS_ID=UA-XXXXX-Y
NEXT_PUBLIC_API_URL=https://api.example.com
```

### Accessing Variables on the Server-Side

```jsx
// pages/api/hello.js
export default function handler(req, res) {
  const dbHost = process.env.DB_HOST;
  console.log('Database Host:', dbHost); // localhost

  const analyticsId = process.env.NEXT_PUBLIC_ANALYTICS_ID;
  console.log('Analytics ID:', analyticsId); // UA-XXXXX-Y

  res.status(200).json({ message: 'Hello' });
}
```

### Accessing Variables on the Client-Side

```jsx
// pages/index.js
function HomePage() {
  const analyticsId = process.env.NEXT_PUBLIC_ANALYTICS_ID;
  const apiUrl = process.env.NEXT_PUBLIC_API_URL;

  return (
    <div>
      <h1>Analytics ID: {analyticsId}</h1>
      <p>API URL: {apiUrl}</p>
    </div>
  );
}

export default HomePage;
```

## Resources

*   **Article:** [Next.js Docs - Environment Variables](https://nextjs.org/docs/basic-features/environment-variables)
*   **Video:** [Next.js Environment Variables Tutorial - Traversy Media](https://www.youtube.com/watch?v=K7C_0_2_200)
