
# 6. CSS Variables (Custom Properties)

## Quick Revision

**CSS Variables**, officially known as **CSS Custom Properties**, allow you to define reusable values throughout your stylesheets. They are defined with a `--` prefix (e.g., `--primary-color: #3498db;`) and accessed using the `var()` function (e.g., `color: var(--primary-color);`).

Unlike preprocessor variables (Sass, LESS), CSS variables are live and can be manipulated with JavaScript, making them powerful for dynamic styling and theming.

## Detailed Explanation

Before CSS variables, if you wanted to reuse a value (like a brand color) across your stylesheet, you had to use a CSS preprocessor. CSS variables bring this functionality natively to the browser.

### How CSS Variables Work

1.  **Declaration:** Custom properties are declared inside a selector, typically `:root` to make them globally available.

    ```css
    :root {
      --primary-color: #007bff;
      --font-size-base: 16px;
    }
    ```

2.  **Usage:** You access the value of a custom property using the `var()` function.

    ```css
    body {
      background-color: var(--primary-color);
      font-size: var(--font-size-base);
    }
    ```

3.  **Inheritance:** Custom properties are inherited. If you define a variable on a parent element, its children can use it.

4.  **Fallback Values:** The `var()` function can accept a second argument, which is a fallback value to use if the custom property is not defined.

    ```css
    color: var(--undefined-color, black); /* Will use black if --undefined-color is not set */
    ```

### Benefits of CSS Variables

*   **Maintainability:** Change a value in one place, and it updates everywhere.
*   **Theming:** Easily switch themes (e.g., light/dark mode) by changing a few variable values.
*   **Dynamic Styling:** Manipulate CSS properties directly with JavaScript.
*   **Readability:** Makes your CSS more semantic and easier to understand.

## Code Examples

### Basic Usage and Theming

```html
<div class="theme-light">
  <h1>Welcome</h1>
  <p>This is some content.</p>
  <button>Click Me</button>
</div>

<div class="theme-dark">
  <h1>Welcome</h1>
  <p>This is some content.</p>
  <button>Click Me</button>
</div>

<style>
  :root {
    --text-color: #333;
    --background-color: #fff;
    --button-bg: #007bff;
    --button-text: #fff;
  }

  .theme-dark {
    --text-color: #eee;
    --background-color: #333;
    --button-bg: #663399;
  }

  body {
    font-family: sans-serif;
  }

  div {
    padding: 20px;
    margin: 10px;
    border: 1px solid var(--text-color);
    background-color: var(--background-color);
    color: var(--text-color);
  }

  h1 {
    color: var(--text-color);
  }

  button {
    background-color: var(--button-bg);
    color: var(--button-text);
    padding: 10px 15px;
    border: none;
    cursor: pointer;
  }
</style>
```

### Manipulating with JavaScript

```html
<button id="changeTheme">Toggle Theme</button>

<style>
  :root {
    --primary-color: blue;
  }
  .box {
    width: 100px;
    height: 100px;
    background-color: var(--primary-color);
  }
</style>

<div class="box"></div>

<script>
  const button = document.getElementById('changeTheme');
  const root = document.documentElement; // Represents the :root element

  button.addEventListener('click', () => {
    const currentColor = getComputedStyle(root).getPropertyValue('--primary-color').trim();
    if (currentColor === 'blue') {
      root.style.setProperty('--primary-color', 'red');
    } else {
      root.style.setProperty('--primary-color', 'blue');
    }
  });
</script>
```

## Resources

*   **Article:** [MDN - CSS custom properties (variables)](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)
*   **Article:** [CSS-Tricks - A Complete Guide to Custom Properties](https://css-tricks.com/a-complete-guide-to-custom-properties/)
*   **Video:** [CSS Variables Explained - Kevin Powell](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
