
# 11. Pre-rendering in Next.js

## Quick Revision

**Pre-rendering** is a core concept in Next.js where HTML is generated for a page in advance, rather than having it all done by client-side JavaScript. This results in better performance and improved SEO.

Next.js supports two forms of pre-rendering:

*   **Static Site Generation (SSG):** HTML is generated at **build time**.
*   **Server-Side Rendering (SSR):** HTML is generated on the **server for each request**.

## Detailed Explanation

By default, Next.js pre-renders every page. This means that instead of having an empty HTML file and then populating it with JavaScript on the client-side (Client-Side Rendering - CSR), Next.js generates the HTML for each page in advance.

### Why Pre-rendering?

*   **Better Performance:** Users see the content of the page faster because the HTML is already there.
*   **Improved SEO:** Search engine crawlers can easily index the content of the page because the full HTML is available.

### Static Site Generation (SSG)

*   **How it works:** The HTML is generated at build time. This means that when you run `next build`, Next.js will generate the HTML for all of your static pages.
*   **Data fetching:** Uses `getStaticProps` to fetch data at build time.
*   **When to use:** For pages that don't change frequently, such as blogs, marketing pages, or documentation.

### Server-Side Rendering (SSR)

*   **How it works:** The HTML is generated on the server for each request. This means that when a user requests a page, Next.js will generate the HTML on the server and send it to the client.
*   **Data fetching:** Uses `getServerSideProps` to fetch data on each request.
*   **When to use:** For pages that need to display frequently updated data or user-specific data.

### Client-Side Hydration

After the pre-rendered HTML is sent to the browser, the browser downloads the JavaScript bundle. React then "hydrates" the existing HTML, making the page interactive. This process is called **hydration**.

## Code Examples

### SSG Example (`getStaticProps`)

```jsx
// pages/index.js
function HomePage({ posts }) {
  return (
    <div>
      <h1>Welcome to my blog!</h1>
      <ul>
        {posts.map((post) => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </div>
  );
}

export async function getStaticProps() {
  // Data is fetched at build time
  const res = await fetch('https://api.example.com/posts');
  const posts = await res.json();

  return {
    props: {
      posts,
    },
  };
}

export default HomePage;
```

### SSR Example (`getServerSideProps`)

```jsx
// pages/dashboard.js
function Dashboard({ user }) {
  return (
    <div>
      <h1>Welcome, {user.name}</h1>
      <p>Your email: {user.email}</p>
    </div>
  );
}

export async function getServerSideProps(context) {
  // Data is fetched on each request
  const res = await fetch(`https://api.example.com/users/${context.req.cookies.userId}`);
  const user = await res.json();

  return {
    props: {
      user,
    },
  };
}

export default Dashboard;
```

## Resources

*   **Article:** [Next.js Docs - Pre-rendering](https://nextjs.org/docs/basic-features/data-fetching/overview)
*   **Video:** [Next.js Pre-rendering Explained - Fireship](https://www.youtube.com/watch?v=9Q_J0_0200Q)
