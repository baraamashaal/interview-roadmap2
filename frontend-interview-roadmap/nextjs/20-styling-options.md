
# 20. Styling Options in Next.js

## Quick Revision

Next.js supports various styling methods, offering flexibility to developers. The most common approaches include:

*   **CSS Modules:** Locally scoped CSS classes, preventing naming conflicts.
*   **Styled JSX:** Built-in CSS-in-JS solution for component-scoped styles.
*   **Sass/SCSS:** Preprocessor support for advanced CSS features.
*   **Tailwind CSS:** A utility-first CSS framework.
*   **CSS-in-JS Libraries:** Such as Styled Components or Emotion.

## Detailed Explanation

Next.js is unopinionated about how you style your applications, allowing you to choose the method that best suits your project and team.

### 1. CSS Modules

*   **How it works:** CSS Modules automatically scope CSS class names to the component, preventing naming collisions. Files are named `[name].module.css`.
*   **Benefits:** Local scope, no global conflicts, easy to use.
*   **When to use:** Recommended for component-level styling.

### 2. Styled JSX

*   **How it works:** Styled JSX is a CSS-in-JS library built into Next.js. It allows you to write CSS directly within your components using a `<style jsx>` tag. Styles are automatically scoped to the component.
*   **Benefits:** Component-scoped styles, no extra configuration needed.
*   **When to use:** For component-level styling, especially if you prefer writing CSS directly in your components.

### 3. Sass/SCSS

*   **How it works:** Next.js has built-in support for Sass/SCSS. You just need to install `sass` and then you can import `.scss` or `.sass` files.
*   **Benefits:** Variables, nesting, mixins, and other Sass features.
*   **When to use:** For larger projects that require more advanced CSS features and organization.

### 4. Tailwind CSS

*   **How it works:** Tailwind CSS is a utility-first CSS framework that provides a set of low-level utility classes that you can use to build custom designs directly in your markup.
*   **Benefits:** Rapid UI development, highly customizable, small file size with PurgeCSS.
*   **When to use:** When you prefer a utility-first approach and want to avoid writing custom CSS.

### 5. CSS-in-JS Libraries

*   **How it works:** Libraries like Styled Components and Emotion allow you to write CSS directly in your JavaScript components, creating dynamic and component-scoped styles.
*   **Benefits:** Dynamic styling, component-scoped, powerful theming capabilities.
*   **When to use:** When you need advanced dynamic styling or prefer a JavaScript-centric approach to styling.

## Code Examples

### CSS Modules

```jsx
// styles/Home.module.css
.container {
  padding: 20px;
  background-color: #f0f0f0;
}

.title {
  color: #333;
}

// pages/index.js
import styles from '../styles/Home.module.css';

function HomePage() {
  return (
    <div className={styles.container}>
      <h1 className={styles.title}>Welcome!</h1>
    </div>
  );
}
```

### Styled JSX

```jsx
function HomePage() {
  return (
    <div>
      <h1>Hello world</h1>
      <p>Styled JSX is cool</p>
      <style jsx>{`
        h1 {
          color: blue;
        }
        p {
          color: green;
        }
      `}</style>
    </div>
  );
}
```

### Sass/SCSS

```scss
// styles/variables.scss
$primary-color: #0070f3;

// styles/Button.module.scss
.button {
  background-color: $primary-color;
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
}

// components/Button.js
import styles from '../styles/Button.module.scss';

function Button() {
  return <button className={styles.button}>Click Me</button>;
}
```

## Resources

*   **Article:** [Next.js Docs - Styling](https://nextjs.org/docs/basic-features/built-in-css-support)
*   **Framework:** [Tailwind CSS](https://tailwindcss.com/)
*   **Library:** [Styled Components](https://styled-components.com/)
*   **Library:** [Emotion](https://emotion.sh/docs/introduction)
