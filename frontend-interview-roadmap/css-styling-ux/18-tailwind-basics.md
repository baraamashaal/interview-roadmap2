
# 18. Tailwind CSS Basics

## Quick Revision

**Tailwind CSS** is a utility-first CSS framework that provides a set of low-level utility classes that you can use to build custom designs directly in your markup. Instead of writing custom CSS for every component, you compose designs by applying these utility classes directly to your HTML elements.

## Detailed Explanation

Traditional CSS frameworks (like Bootstrap) come with pre-designed components (buttons, cards, navbars). While this speeds up development, it often leads to generic-looking websites and can be difficult to customize without overriding styles.

Tailwind CSS takes a different approach. It doesn't provide pre-built components. Instead, it gives you a comprehensive set of utility classes that map directly to CSS properties.

### Key Concepts

1.  **Utility-First:** You build your designs by composing utility classes directly in your HTML.

    ```html
    <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
      Click Me
    </button>
    ```

2.  **Responsive Design:** Tailwind makes responsive design easy with responsive prefixes (e.g., `sm:`, `md:`, `lg:`).

    ```html
    <div class="w-full md:w-1/2 lg:w-1/3"></div>
    ```

3.  **Customization:** Tailwind is highly customizable. You can configure your design system (colors, fonts, spacing, breakpoints) in `tailwind.config.js`.

4.  **PurgeCSS:** Tailwind works with PurgeCSS (or its built-in JIT mode) to remove all unused CSS classes from your production build, resulting in extremely small CSS file sizes.

### Benefits

*   **Rapid UI Development:** Build complex UIs much faster without writing custom CSS.
*   **No Naming Conflicts:** Utility classes are atomic, so you don't have to worry about naming conventions or global CSS conflicts.
*   **Highly Customizable:** Easily adapt the design system to your brand.
*   **Small File Sizes:** PurgeCSS ensures only the used utility classes are included in the final bundle.
*   **Consistency:** Encourages a consistent design system across your application.

### Downsides

*   **Verbose HTML:** Markup can become cluttered with many utility classes.
*   **Learning Curve:** Requires learning Tailwind's utility class names.
*   **Not for everyone:** Some developers prefer writing semantic CSS.

## Code Example

### Setting up Tailwind CSS (Conceptual)

1.  **Install:** `npm install -D tailwindcss postcss autoprefixer`
2.  **Initialize:** `npx tailwindcss init -p` (creates `tailwind.config.js` and `postcss.config.js`)
3.  **Configure `tailwind.config.js`:**

    ```javascript
    // tailwind.config.js
    module.exports = {
      content: [
        "./pages/**/*.{js,ts,jsx,tsx}",
        "./components/**/*.{js,ts,jsx,tsx}",
      ],
      theme: {
        extend: {},
      },
      plugins: [],
    }
    ```

4.  **Add Tailwind directives to your CSS:**

    ```css
    /* styles/globals.css */
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
    ```

5.  **Import `globals.css` into `pages/_app.js`:**

    ```jsx
    // pages/_app.js
    import '../styles/globals.css';

    function MyApp({ Component, pageProps }) {
      return <Component {...pageProps} />;
    }

    export default MyApp;
    ```

### Using Tailwind Classes in a Component

```jsx
function Card() {
  return (
    <div className="max-w-sm rounded overflow-hidden shadow-lg m-4">
      <img className="w-full" src="/img/card-top.jpg" alt="Sunset in the mountains" />
      <div className="px-6 py-4">
        <div className="font-bold text-xl mb-2">The Coldest Sunset</div>
        <p className="text-gray-700 text-base">
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, nulla! Maiores et perferendis eaque, exercitationem praesentium nihil.
        </p>
      </div>
      <div className="px-6 pt-4 pb-2">
        <span className="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">#photography</span>
        <span className="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">#travel</span>
        <span className="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mb-2">#winter</span>
      </div>
    </div>
  );
}
```

## Resources

*   **Official Site:** [Tailwind CSS](https://tailwindcss.com/)
*   **Documentation:** [Tailwind CSS Docs](https://tailwindcss.com/docs)
*   **Video:** [Tailwind CSS Crash Course - Traversy Media](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
