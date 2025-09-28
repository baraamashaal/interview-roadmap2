
# 3. API Routes in Next.js

## Quick Revision

**API Routes** in Next.js allow you to build your own API endpoints as part of your Next.js application. They are server-side functions that run in a Node.js environment, not in the browser. This means you can handle server-side logic, interact with databases, and securely manage sensitive data without needing a separate backend server.

## Detailed Explanation

API Routes are a powerful feature of Next.js that enable you to create a full-stack application within a single project. They reside in the `pages/api` directory and are mapped to `/api/*` endpoints.

### How API Routes Work

1.  Any file inside `pages/api` is treated as an API endpoint instead of a page.
2.  These files export a default function that takes `req` (request) and `res` (response) objects as arguments, similar to an Express.js handler.
3.  The code inside API Routes runs on the server-side, meaning it will not be part of your client-side bundle.

### Key Features

*   **Server-side execution:** Ideal for handling sensitive data, database queries, and authentication.
*   **Zero configuration:** No need to set up a separate server or routing.
*   **Full control over response:** You can send JSON, HTML, or any other type of response.
*   **Integration with Next.js data fetching:** Can be used to provide data for `getStaticProps` or `getServerSideProps`.

## Code Examples

### Basic API Route

Create a file `pages/api/hello.js`:

```javascript
// pages/api/hello.js
export default function handler(req, res) {
  res.status(200).json({ name: 'John Doe' });
}
```

Now, if you visit `/api/hello` in your browser, you will see `{"name":"John Doe"}`.

### Handling Different HTTP Methods

You can handle different HTTP methods (GET, POST, PUT, DELETE) within the same API route.

```javascript
// pages/api/users.js
export default function handler(req, res) {
  if (req.method === 'POST') {
    // Process a POST request
    res.status(200).json({ message: 'User created', body: req.body });
  } else if (req.method === 'GET') {
    // Handle any other HTTP method
    res.status(200).json({ users: ['Alice', 'Bob'] });
  } else {
    res.setHeader('Allow', ['GET', 'POST']);
    res.status(405).end(`Method ${req.method} Not Allowed`);
  }
}
```

### Dynamic API Routes

You can create dynamic API routes by using square brackets in the file name, similar to dynamic pages.

Create a file `pages/api/user/[id].js`:

```javascript
// pages/api/user/[id].js
export default function handler(req, res) {
  const { id } = req.query;
  res.status(200).json({ id, name: `User ${id}` });
}
```

Now, `/api/user/1` will return `{"id":"1","name":"User 1"}`.

## Use Cases

*   **Building a backend for your frontend:** Handle database interactions, authentication, and other server-side logic.
*   **Proxying requests:** Hide API keys or sensitive information from the client by making requests through an API route.
*   **Form submissions:** Process form data securely on the server.

## Resources

*   **Article:** [Next.js Docs - API Routes](https://nextjs.org/docs/api-routes/introduction)
*   **Video:** [Next.js API Routes Tutorial - Traversy Media](https://www.youtube.com/watch?v=K7C_0_2_200)
