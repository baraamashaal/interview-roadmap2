
# 10. Specificity Rules in CSS

## Quick Revision

**Specificity** is the algorithm CSS uses to determine which CSS declaration applies to an element when multiple declarations could apply. It's essentially a scoring system that dictates which style rule "wins" when there's a conflict.

Specificity is calculated based on the type of selectors used:

1.  **Inline Styles:** Highest specificity.
2.  **IDs:** High specificity.
3.  **Classes, Attributes, Pseudo-classes:** Medium specificity.
4.  **Elements, Pseudo-elements:** Lowest specificity.

## Detailed Explanation

When multiple CSS rules target the same element and try to apply conflicting styles, the browser uses specificity to decide which rule's styles should be applied. The rule with the highest specificity wins.

### How Specificity is Calculated

Specificity is calculated as a score, often represented as four comma-separated values: `(a, b, c, d)`.

*   **`a` (Inline Styles):** If a style is applied directly to an element using the `style` attribute, `a = 1`. Otherwise, `a = 0`.
*   **`b` (IDs):** Count the number of ID selectors (e.g., `#my-id`).
*   **`c` (Classes, Attributes, Pseudo-classes):** Count the number of class selectors (e.g., `.my-class`), attribute selectors (e.g., `[type="text"]`), and pseudo-classes (e.g., `:hover`, `:nth-child`).
*   **`d` (Elements, Pseudo-elements):** Count the number of element selectors (e.g., `div`, `p`) and pseudo-elements (e.g., `::before`, `::after`).

**Example:**

*   `p` -> `(0, 0, 0, 1)`
*   `.my-class` -> `(0, 0, 1, 0)`
*   `#my-id` -> `(0, 1, 0, 0)`
*   `div.my-class` -> `(0, 0, 1, 1)`
*   `#my-id p` -> `(0, 1, 0, 1)`

**Comparison:** The scores are compared from left to right. The first higher value wins. For example, `(0, 1, 0, 0)` is more specific than `(0, 0, 10, 10)`.

### The `!important` Rule

The `!important` keyword can be added to a CSS declaration to override any other declarations, regardless of specificity. However, it is generally considered bad practice and should be used sparingly, as it can make CSS difficult to debug and maintain.

### Order of Appearance

If two rules have the exact same specificity, the one that appears later in the stylesheet (or is loaded later) will take precedence.

## Code Examples

```html
<style>
  /* Specificity: (0, 0, 0, 1) */
  p {
    color: red;
  }

  /* Specificity: (0, 0, 1, 0) */
  .my-paragraph {
    color: blue;
  }

  /* Specificity: (0, 1, 0, 0) */
  #unique-paragraph {
    color: green;
  }

  /* Specificity: (0, 0, 1, 1) */
  div p {
    color: purple;
  }

  /* Specificity: (0, 0, 2, 0) */
  .container .my-paragraph {
    color: orange;
  }

  /* Specificity: (0, 1, 0, 1) */
  #parent-div p {
    color: brown;
  }

  /* Specificity: (1, 0, 0, 0) */
  .inline-style-example {
    color: black !important; /* !important overrides everything */
  }
</style>

<div id="parent-div">
  <p style="color: gray;" class="my-paragraph inline-style-example" id="unique-paragraph">This is a paragraph.</p>
</div>
```

**What color will the paragraph be?**

1.  `#unique-paragraph` -> `(0, 1, 0, 0)` -> green
2.  `.container .my-paragraph` -> `(0, 0, 2, 0)` -> orange
3.  `#parent-div p` -> `(0, 1, 0, 1)` -> brown
4.  `.my-paragraph` -> `(0, 0, 1, 0)` -> blue
5.  `p` -> `(0, 0, 0, 1)` -> red
6.  Inline style `style="color: gray;"` -> `(1, 0, 0, 0)` -> gray
7.  `.inline-style-example` with `!important` -> `(0, 0, 1, 0)` + `!important` -> black

The `!important` rule on `.inline-style-example` will win, making the text **black**.

If `!important` was not present, the inline style `(1, 0, 0, 0)` would win, making the text gray.

## Resources

*   **Article:** [MDN - Specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)
*   **Article:** [CSS-Tricks - Specificity](https://css-tricks.com/specifics-on-css-specificity/)
*   **Video:** [CSS Specificity Explained - Kevin Powell](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
