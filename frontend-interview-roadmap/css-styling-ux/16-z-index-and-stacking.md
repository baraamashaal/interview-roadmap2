
# 16. `z-index` and Stacking Contexts in CSS

## Quick Revision

**`z-index`** is a CSS property that controls the vertical stacking order of positioned elements that overlap. Elements with a higher `z-index` value are displayed in front of elements with a lower `z-index` value.

However, `z-index` only works within the same **stacking context**. Understanding stacking contexts is crucial for predicting how `z-index` will behave.

## Detailed Explanation

### The `z-index` Property

*   **Requires `position`:** `z-index` only affects elements that have a `position` value other than `static` (i.e., `relative`, `absolute`, `fixed`, or `sticky`).
*   **Integer values:** `z-index` accepts integer values (e.g., `1`, `10`, `-1`). Higher numbers mean closer to the user.

### Stacking Contexts

A **stacking context** is a three-dimensional conceptual rendering of HTML elements, along an imaginary z-axis relative to the user who is assumed to be facing the viewport or the page. HTML elements are rendered in a specific order, primarily determined by their position in the document tree, their `z-index` value, and the stacking context they belong to.

**How a Stacking Context is Created:**

A new stacking context is created by an element when it has:

*   `position: absolute` or `relative` with a `z-index` value other than `auto`.
*   `position: fixed` or `sticky`.
*   `opacity` less than 1.
*   `transform`, `filter`, `perspective`, `clip-path`, `mask`, `mask-image`, `mask-border` with a value other than `none`.
*   `will-change` with `opacity`, `transform`, `filter`, `perspective`, `clip-path`, or `mask`.
*   `display: flex` or `grid` with `z-index` other than `auto` on its child items.

**Key Rule:** `z-index` values only compare elements within the same stacking context. An element's `z-index` value is only meaningful in relation to other elements within the same stacking context. A child element cannot break out of its parent's stacking context.

## Code Examples

### Basic `z-index` Example

```html
<div class="box red"></div>
<div class="box blue"></div>

<style>
  .box {
    width: 100px;
    height: 100px;
    position: absolute;
  }
  .red {
    background-color: red;
    left: 50px;
    top: 50px;
    z-index: 1;
  }
  .blue {
    background-color: blue;
    left: 80px;
    top: 80px;
    z-index: 2; /* Blue box will be on top of red */
  }
</style>
```

### Stacking Context Example

```html
<div class="container container-1">
  <div class="item item-a">Item A (z-index: 1)</div>
  <div class="item item-b">Item B (z-index: 100)</div>
</div>

<div class="container container-2">
  <div class="item item-c">Item C (z-index: 2)</div>
</div>

<style>
  .container {
    position: relative; /* Creates a new stacking context */
    width: 200px;
    height: 200px;
    border: 2px solid black;
    margin: 20px;
  }
  .item {
    width: 80px;
    height: 80px;
    position: absolute;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .item-a {
    background-color: red;
    left: 10px;
    top: 10px;
    z-index: 1;
  }
  .item-b {
    background-color: blue;
    left: 30px;
    top: 30px;
    z-index: 100;
  }
  .item-c {
    background-color: green;
    left: 10px;
    top: 10px;
    z-index: 2;
  }
</style>
```

**Explanation:**

*   Item B (z-index 100) is on top of Item A (z-index 1) because they are in the same stacking context (`container-1`).
*   Item C (z-index 2) is on top of both Item A and Item B, even though its `z-index` is lower than Item B's. This is because Item C is in a *different* stacking context (`container-2`), and stacking contexts are compared as a whole.

## Resources

*   **Article:** [MDN - Stacking context](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_positioned_layout/Understanding_z-index/The_stacking_context)
*   **Article:** [CSS-Tricks - What No One Told You About Z-Index](https://css-tricks.com/what-no-one-told-you-about-z-index/)
*   **Video:** [CSS Z-Index Explained - Kevin Powell](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
