
# 15. Web Accessibility (A11y)

## Quick Revision

**Web accessibility (a11y)** refers to the practice of making websites usable by everyone, regardless of their abilities or disabilities. This includes people with visual, auditory, physical, speech, cognitive, and neurological disabilities. Accessible websites benefit all users, improving overall usability and SEO.

Key principles of web accessibility are defined by the **WCAG (Web Content Accessibility Guidelines)**:

*   **Perceivable:** Information and UI components must be presentable to users in ways they can perceive.
*   **Operable:** UI components and navigation must be operable.
*   **Understandable:** Information and the operation of the user interface must be understandable.
*   **Robust:** Content must be robust enough that it can be interpreted reliably by a wide variety of user agents, including assistive technologies.

## Detailed Explanation

Building accessible websites is not just about compliance; it's about creating inclusive experiences for all users. Many accessibility features also improve the user experience for everyone.

### 1. Semantic HTML

Using semantic HTML elements (e.g., `<header>`, `<nav>`, `<main>`, `<article>`, `<aside>`, `<footer>`, `<button>`) is the foundation of accessibility. Semantic elements convey meaning to both browsers and assistive technologies.

*   **Do:** Use `<button>` for buttons, `<a href="...">` for links.
*   **Don't:** Use `<div>` with `onClick` for buttons.

### 2. ARIA Attributes

**ARIA (Accessible Rich Internet Applications)** attributes provide additional semantics to HTML elements, especially for dynamic content and custom UI components that are not natively accessible. ARIA roles, states, and properties help assistive technologies understand the purpose and state of elements.

*   **`role`:** Defines the role of an element (e.g., `role="button"`, `role="dialog"`).
*   **`aria-label`:** Provides a text label for an element when no visible label is present.
*   **`aria-labelledby`:** Refers to the ID of an element that serves as a label.
*   **`aria-describedby`:** Refers to the ID of an element that describes the current element.
*   **`aria-live`:** Indicates that an element will be updated, and describes the types of updates the user agent, aassistive technologies, and user can expect.

### 3. Keyboard Navigation

Many users rely on keyboard navigation. Ensure all interactive elements are reachable and operable using the keyboard.

*   **`tabindex`:** Controls whether an element is focusable and its order in the tab sequence.
    *   `tabindex="0"`: Makes an element focusable and places it in the natural tab order.
    *   `tabindex="-1"`: Makes an element focusable but removes it from the natural tab order (can be focused programmatically).
    *   `tabindex="positive_number"`: Not recommended, as it can create confusing tab orders.

### 4. Color Contrast

Ensure sufficient color contrast between text and its background. WCAG guidelines recommend a contrast ratio of at least 4.5:1 for normal text and 3:1 for large text.

### 5. Alternative Text for Images

Provide meaningful `alt` text for all `<img>` tags. This text is read by screen readers and displayed if the image fails to load.

```html
<img src="logo.png" alt="Company logo">
```

### 6. Form Accessibility

*   **Labels:** Always associate labels with form inputs using the `for` and `id` attributes.
*   **Error messages:** Provide clear and accessible error messages.

## Code Examples

### Semantic HTML and ARIA

```html
<header>
  <nav aria-label="Main navigation">
    <ul>
      <li><a href="/">Home</a></li>
      <li><a href="/about">About</a></li>
    </ul>
  </nav>
</header>

<main>
  <button type="button" aria-expanded="false" aria-controls="menu-popup">
    Toggle Menu
  </button>
  <div id="menu-popup" role="menu" hidden>
    <!-- Menu items -->
  </div>

  <form aria-labelledby="login-heading">
    <h2 id="login-heading">Login</h2>
    <div>
      <label for="username">Username:</label>
      <input type="text" id="username" name="username" aria-required="true">
    </div>
    <div>
      <label for="password">Password:</label>
      <input type="password" id="password" name="password" aria-required="true">
    </div>
    <button type="submit">Submit</button>
  </form>
</main>
```

## Tools for Accessibility

*   **Lighthouse:** Built into Chrome DevTools, provides an accessibility audit.
*   **axe DevTools:** Browser extension for automated accessibility testing.
*   **Screen Readers:** Test with actual screen readers (NVDA, JAWS, VoiceOver).
*   **Keyboard Navigation:** Test your site using only the keyboard.

## Resources

*   **Official Guide:** [WCAG (Web Content Accessibility Guidelines)](https://www.w3.org/WAI/WCAG21/quickref/)
*   **Article:** [MDN - Accessibility](https://developer.mozilla.org/en-US/docs/Web/Accessibility)
*   **Article:** [A11y Project](https://www.a11yproject.com/)
*   **Video:** [Web Accessibility Basics - Google Chrome Developers](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
