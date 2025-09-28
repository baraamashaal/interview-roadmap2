
# 30. Migration to Next.js

## Quick Revision

Migrating an existing React application (especially one built with Create React App - CRA) to Next.js involves transitioning from a client-side rendered (CSR) architecture to a framework that supports server-side rendering (SSR), static site generation (SSG), and other advanced features. The process typically involves restructuring your project, adapting data fetching, and configuring Next.js-specific features.

## Detailed Explanation

Migrating to Next.js can bring significant benefits in terms of performance, SEO, and developer experience, but it requires careful planning and execution.

### Common Migration Scenarios

1.  **From Create React App (CRA):** This is a very common migration path, as many projects start with CRA for its simplicity.
2.  **From a custom Webpack/Babel setup:** More complex, but the principles are similar.

### Key Steps in Migration

#### 1. Project Setup

*   **Install Next.js:** Add `next`, `react`, and `react-dom` to your project dependencies.
*   **Create `pages` directory:** Move your existing React components into the `pages` directory to establish file-system based routing.
*   **Update `package.json` scripts:** Add `next dev`, `next build`, and `next start` scripts.

#### 2. Routing

*   **Replace client-side router:** If you were using `react-router-dom`, you'll need to replace its usage with Next.js's file-system based routing and the `next/link` component.
*   **Dynamic routes:** Convert any dynamic routes from your old router to Next.js's dynamic routing (`[param].js`).

#### 3. Data Fetching

This is often the most significant change.

*   **Identify data fetching needs:** Determine which pages need SSG (`getStaticProps`), SSR (`getServerSideProps`), or client-side fetching.
*   **Refactor data fetching logic:** Move server-side data fetching into `getStaticProps` or `getServerSideProps`.
*   **Client-side fetching:** For data that needs to be fetched on the client, you can continue to use `useEffect` or libraries like SWR/React Query.

#### 4. Styling

*   Next.js supports various styling methods (CSS Modules, Tailwind CSS, Styled JSX, CSS-in-JS). Choose the one that best fits your project and migrate your existing styles.

#### 5. Asset Management

*   **Static assets:** Place static assets (images, fonts) in the `public` directory.
*   **Image Optimization:** Replace `<img>` tags with the `next/image` component for automatic optimization.

#### 6. API Routes

*   If your application has a separate backend, you can keep it or migrate some of its functionality to Next.js API Routes.

#### 7. Environment Variables

*   Configure environment variables using Next.js's `.env` file support, ensuring sensitive variables are not exposed to the client.

## Code Example (Conceptual Migration from CRA)

**Before (CRA):**

```jsx
// src/App.js
import React, { useState, useEffect } from 'react';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

function HomePage() {
  const [data, setData] = useState(null);
  useEffect(() => {
    fetch('/api/data').then(res => res.json()).then(setData);
  }, []);
  return <h1>Home Page {data && data.message}</h1>;
}

function AboutPage() {
  return <h1>About Page</h1>;
}

function App() {
  return (
    <Router>
      <Switch>
        <Route path="/" exact component={HomePage} />
        <Route path="/about" component={AboutPage} />
      </Switch>
    </Router>
  );
}

export default App;
```

**After (Next.js):**

```jsx
// pages/index.js
function HomePage({ message }) {
  return <h1>Home Page {message}</h1>;
}

export async function getServerSideProps() {
  // Data fetching now happens on the server
  const res = await fetch('http://localhost:3000/api/data'); // Assuming API Route
  const data = await res.json();
  return { props: { message: data.message } };
}

export default HomePage;

// pages/about.js
function AboutPage() {
  return <h1>About Page</h1>;
}

export default AboutPage;

// pages/api/data.js (new API Route)
export default function handler(req, res) {
  res.status(200).json({ message: 'from API Route' });
}
```

## Resources

*   **Article:** [Next.js Docs - Migrating from Create React App](https://nextjs.org/docs/migrating/from-create-react-app)
*   **Video:** [Migrate React App to Next.js - Traversy Media](https://www.youtube.com/watch?v=K7C_0_2_200)
