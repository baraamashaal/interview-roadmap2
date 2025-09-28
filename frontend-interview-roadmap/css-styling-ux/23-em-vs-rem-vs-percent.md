
# 23. `em` vs. `rem` vs. `%` in CSS

## Quick Revision

`em`, `rem`, and `%` are all relative units in CSS, meaning their computed value depends on other values. Understanding their differences is crucial for creating scalable and maintainable typography and layouts.

*   **`em`:** Relative to the `font-size` of its **parent element**.
*   **`rem`:** Relative to the `font-size` of the **root HTML element** (`<html>`).
*   **`%` (Percentage):** Relative to the parent element's corresponding property (e.g., `width: 50%` is 50% of the parent's width; `font-size: 150%` is 150% of the parent's font size).

## Detailed Explanation

### 1. `em` Unit

*   **Relative to:** The `font-size` of the element's direct parent.
*   **Behavior:** If an element has a `font-size` of `16px`, then `1em` inside that element will be `16px`. If its parent has a `font-size` of `20px`, then `1em` inside the parent will be `20px`.
*   **Cascading Effect:** `em` units can lead to a compounding effect where font sizes (or other properties) become progressively larger or smaller down the document tree, making it harder to predict and control.
*   **Use Cases:** Good for properties that should scale relative to the current element's font size, such as `line-height`, `padding`, or `margin` within a component.

### 2. `rem` Unit

*   **Relative to:** The `font-size` of the **root HTML element** (`<html>`). By default, most browsers set the root `font-size` to `16px`.
*   **Behavior:** `1rem` will always be equal to the `font-size` of the `<html>` element, regardless of the parent element's font size.
*   **Predictability:** More predictable and easier to manage than `em` because it avoids the compounding effect.
*   **Use Cases:** Ideal for global typography, spacing, and responsive layouts where you want consistent scaling across the entire document.

### 3. `%` (Percentage) Unit

*   **Relative to:** The parent element's corresponding property.
*   **Behavior:** `width: 50%` means 50% of the parent's width. `font-size: 150%` means 150% of the parent's font size.
*   **Use Cases:** Primarily used for fluid layouts (widths, heights, margins, padding) that need to adapt to the parent's dimensions. Can also be used for font sizes, but `rem` is often preferred for typography due to its direct relation to the root.

## Code Examples

### `em` vs. `rem`

```html
<div class="parent">
  Parent (font-size: 20px)
  <p class="em-text">This text uses em.</p>
  <p class="rem-text">This text uses rem.</p>
  <div class="child">
    Child (font-size: 16px)
    <p class="em-text">This text uses em.</p>
    <p class="rem-text">This text uses rem.</p>
  </div>
</div>

<style>
  html {
    font-size: 16px; /* Default root font size */
  }
  .parent {
    font-size: 20px;
    border: 1px solid blue;
    padding: 1em; /* 20px */
    margin-bottom: 20px;
  }
  .child {
    font-size: 16px;
    border: 1px solid green;
    padding: 1em; /* 16px */
    margin-top: 1em; /* 16px */
  }
  .em-text {
    font-size: 1.2em; /* 1.2 * parent's font-size */
    /* In .parent: 1.2 * 20px = 24px */
    /* In .child: 1.2 * 16px = 19.2px */
  }
  .rem-text {
    font-size: 1.2rem; /* 1.2 * html font-size (16px) = 19.2px */
  }
</style>
```

### Percentage Example

```html
<div class="container">
  <div class="box">
    <p>This text uses percentage font-size.</p>
  </div>
</div>

<style>
  .container {
    width: 500px;
    height: 200px;
    background-color: lightgray;
    font-size: 16px;
  }
  .box {
    width: 50%; /* 50% of .container's width (250px) */
    height: 50%; /* 50% of .container's height (100px) */
    background-color: lightblue;
    font-size: 120%; /* 120% of .container's font-size (16px * 1.2 = 19.2px) */
  }
</style>
```

## When to Use Which

*   **`rem`:** Generally preferred for `font-size` to ensure consistent scaling across the entire document based on the root element. Also good for global spacing.
*   **`em`:** Useful for properties like `padding`, `margin`, `line-height` when you want them to scale relative to the current element's `font-size` (e.g., within a button component).
*   **`%`:** Best for fluid layouts where dimensions need to be relative to the parent container's dimensions.

## Resources

*   **Article:** [MDN - CSS Values and Units](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Values_and_Units)
*   **Article:** [CSS-Tricks - `em` vs `rem` vs `px`](https://css-tricks.com/the-difference-between-ems-and-rems/)
*   **Video:** [em vs rem vs px - Kevin Powell](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
