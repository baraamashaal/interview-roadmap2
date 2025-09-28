
# 14. Implementing Dark Mode in Web Applications

## Quick Revision

**Dark mode** (or dark theme) is a display setting for user interfaces that presents light-colored text, icons, and graphical user interface elements on a dark background. It has become a popular feature due to its potential benefits:

*   **Reduced eye strain:** Especially in low-light environments.
*   **Improved battery life:** For devices with OLED screens.
*   **Aesthetic preference:** Many users simply prefer a dark interface.

Implementing dark mode typically involves using CSS variables and the `prefers-color-scheme` media query.

## Detailed Explanation

There are generally two main approaches to implementing dark mode:

1.  **Automatic (System Preference):** Respecting the user's operating system preference for light or dark mode using the `prefers-color-scheme` media query.
2.  **Manual Toggle:** Providing a user interface control (e.g., a button) to allow users to switch between light and dark modes, often persisting their choice.

### 1. Using `prefers-color-scheme` Media Query

This CSS media feature detects if the user has requested the system to use a light or dark color theme.

```css
/* Default light theme styles */
body {
  background-color: #ffffff;
  color: #333333;
}

/* Dark theme styles */
@media (prefers-color-scheme: dark) {
  body {
    background-color: #1a1a1a;
    color: #f0f0f0;
  }
}
```

### 2. Manual Toggle with CSS Variables and JavaScript

For more control and to allow users to override their system preference, you can implement a manual toggle. This often involves:

*   **CSS Variables:** Define your color palette using CSS custom properties (variables) at the `:root` level.
*   **JavaScript:** Toggle a class on the `<body>` or `<html>` element (e.g., `dark-mode`) to switch between themes.

### Best Practices

*   **Provide a toggle:** Always offer a manual toggle, even if you respect system preferences, to give users control.
*   **Persist user choice:** Store the user's preference (e.g., in `localStorage`) so it persists across sessions.
*   **Test thoroughly:** Ensure readability and contrast in both modes.
*   **Consider accessibility:** Ensure sufficient contrast ratios for text and UI elements in both themes.

## Code Examples

### Automatic Dark Mode with `prefers-color-scheme`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Automatic Dark Mode</title>
  <style>
    :root {
      --background-color: #ffffff;
      --text-color: #333333;
    }

    @media (prefers-color-scheme: dark) {
      :root {
        --background-color: #1a1a1a;
        --text-color: #f0f0f0;
      }
    }

    body {
      background-color: var(--background-color);
      color: var(--text-color);
      font-family: sans-serif;
      transition: background-color 0.3s ease, color 0.3s ease;
    }
  </style>
</head>
<body>
  <h1>Hello, World!</h1>
  <p>This page will automatically switch between light and dark themes based on your system preferences.</p>
</body>
</html>
```

### Manual Dark Mode Toggle with JavaScript and CSS Variables

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Manual Dark Mode</title>
  <style>
    :root {
      --background-color: #ffffff;
      --text-color: #333333;
      --button-bg: #007bff;
      --button-text: #ffffff;
    }

    html.dark-mode {
      --background-color: #1a1a1a;
      --text-color: #f0f0f0;
      --button-bg: #663399;
    }

    body {
      background-color: var(--background-color);
      color: var(--text-color);
      font-family: sans-serif;
      transition: background-color 0.3s ease, color 0.3s ease;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }

    button {
      background-color: var(--button-bg);
      color: var(--button-text);
      padding: 10px 20px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      margin-top: 20px;
      transition: background-color 0.3s ease, color 0.3s ease;
    }
  </style>
</head>
<body>
  <h1>Manual Dark Mode Toggle</h1>
  <p>Click the button to switch between light and dark themes.</p>
  <button id="theme-toggle">Toggle Theme</button>

  <script>
    const themeToggle = document.getElementById('theme-toggle');
    const htmlElement = document.documentElement;

    // Check for saved theme preference
    const savedTheme = localStorage.getItem('theme');
    if (savedTheme) {
      htmlElement.classList.add(savedTheme);
    } else if (window.matchMedia('(prefers-color-scheme: dark)').matches) {
      htmlElement.classList.add('dark-mode');
    }

    themeToggle.addEventListener('click', () => {
      if (htmlElement.classList.contains('dark-mode')) {
        htmlElement.classList.remove('dark-mode');
        localStorage.setItem('theme', 'light-mode');
      } else {
        htmlElement.classList.add('dark-mode');
        localStorage.setItem('theme', 'dark-mode');
      }
    });
  </script>
</body>
</html>
```

## Resources

*   **Article:** [MDN - `prefers-color-scheme`](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme)
*   **Article:** [CSS-Tricks - A Complete Guide to Dark Mode on the Web](https://css-tricks.com/a-complete-guide-to-dark-mode-on-the-web/)
*   **Video:** [How to Build a Dark Mode Toggle - Kevin Powell](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
