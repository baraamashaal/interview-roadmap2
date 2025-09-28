
# 7. Pseudo-classes vs. Pseudo-elements in CSS

## Quick Revision

**Pseudo-classes** and **pseudo-elements** are CSS keywords that allow you to apply styles to elements based on their state or to specific parts of an element, respectively.

*   **Pseudo-classes (`:`):** Select elements based on their state or position within the document tree (e.g., `:hover`, `:focus`, `:nth-child`). They select existing elements.

*   **Pseudo-elements (`::`):** Select and style a specific part of an element (e.g., `::before`, `::after`, `::first-line`). They create virtual elements that are not explicitly in the HTML.

## Detailed Explanation

Both pseudo-classes and pseudo-elements extend the capabilities of CSS selectors, allowing for more dynamic and precise styling without altering the HTML structure.

### Pseudo-classes (`:`)

A pseudo-class is used to define a special state of an element. It selects elements that are in a certain state.

**Common Pseudo-classes:**

*   **`:hover`:** Selects an element when the user mouses over it.
*   **`:focus`:** Selects an element when it has received focus.
*   **`:active`:** Selects an element when it is being activated by the user (e.g., clicked).
*   **`:visited`:** Selects links that have been visited by the user.
*   **`:nth-child(n)`:** Selects elements based on their position among a group of siblings.
*   **`:first-child`, `:last-child`:** Selects the first or last child of its parent.
*   **`:not(selector)`:** Selects elements that do not match the specified selector.

### Pseudo-elements (`::`)

A pseudo-element is used to style a specified part of an element. They create an abstract element that is not part of the document tree.

**Common Pseudo-elements:**

*   **`::before`:** Inserts content before the content of an element.
*   **`::after`:** Inserts content after the content of an element.
*   **`::first-line`:** Selects the first line of a block-level element.
*   **`::first-letter`:** Selects the first letter of a block-level element.
*   **`::selection`:** Selects the portion of an element that is highlighted by the user.

**Note:** While the double-colon (`::`) syntax is the standard for pseudo-elements, the single-colon (`:`) syntax is also supported for backward compatibility with older browsers (e.g., `:before` instead of `::before`). It's generally recommended to use `::` for pseudo-elements for clarity.

## Code Examples

### Pseudo-class Example

```html
<button class="my-button">Hover Me</button>
<input type="text" class="my-input" placeholder="Focus Me">

<style>
  .my-button {
    background-color: blue;
    color: white;
    padding: 10px 15px;
    border: none;
    cursor: pointer;
  }
  .my-button:hover {
    background-color: darkblue;
  }

  .my-input {
    border: 1px solid gray;
    padding: 8px;
  }
  .my-input:focus {
    border-color: blue;
    outline: none;
  }

  ul li:nth-child(odd) {
    background-color: #f0f0f0;
  }
</style>
```

### Pseudo-element Example

```html
<p class="quote">This is a very important quote that needs special styling.</p>

<style>
  .quote {
    font-style: italic;
    color: #555;
    position: relative;
    padding-left: 20px;
  }
  .quote::before {
    content: '\201C'; /* Unicode for left double quotation mark */
    font-size: 2em;
    color: #ccc;
    position: absolute;
    left: 0;
    top: 0;
  }
  .quote::after {
    content: '\201D'; /* Unicode for right double quotation mark */
    font-size: 2em;
    color: #ccc;
    position: absolute;
    right: 0;
    bottom: 0;
  }

  h1::first-letter {
    font-size: 2em;
    color: red;
  }
</style>
```

## Resources

*   **Article:** [MDN - Pseudo-classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)
*   **Article:** [MDN - Pseudo-elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements)
*   **Article:** [CSS-Tricks - Pseudo-Class and Pseudo-Element Selectors](https://css-tricks.com/pseudo-class-and-pseudo-element-selectors/)
