
# 2. Flexbox vs. CSS Grid

## Quick Revision

**Flexbox** and **CSS Grid** are powerful CSS layout modules that help you create complex and responsive web designs. While both are used for layout, they are designed for different purposes.

*   **Flexbox (Flexible Box Layout):** A one-dimensional layout system. It excels at distributing space among items in a single row or a single column.

*   **CSS Grid (Grid Layout):** A two-dimensional layout system. It allows you to arrange items in both rows and columns simultaneously, making it ideal for overall page layouts.

## Detailed Explanation

### Flexbox

Flexbox is designed for laying out items in a single dimension, either as a row or as a column. It provides a powerful way to align, distribute, and order items within a container.

**Key Concepts:**

*   **Flex Container:** The parent element with `display: flex`.
*   **Flex Items:** The direct children of the flex container.
*   **Main Axis:** The primary axis along which flex items are laid out (horizontal for `flex-direction: row`, vertical for `flex-direction: column`).
*   **Cross Axis:** The axis perpendicular to the main axis.

**Common Flexbox Properties:**

*   `flex-direction`: `row`, `column`, `row-reverse`, `column-reverse`
*   `justify-content`: `flex-start`, `flex-end`, `center`, `space-between`, `space-around`, `space-evenly`
*   `align-items`: `flex-start`, `flex-end`, `center`, `baseline`, `stretch`
*   `flex-wrap`: `nowrap`, `wrap`, `wrap-reverse`
*   `gap`: Space between flex items

### CSS Grid

CSS Grid is a two-dimensional layout system that allows you to create complex grid-based layouts with rows and columns. It gives you precise control over the placement and sizing of items.

**Key Concepts:**

*   **Grid Container:** The parent element with `display: grid`.
*   **Grid Items:** The direct children of the grid container.
*   **Grid Lines:** The dividing lines that form the grid.
*   **Grid Tracks:** The spaces between grid lines (rows and columns).
*   **Grid Cells:** The smallest unit of the grid.
*   **Grid Areas:** Named areas within the grid.

**Common Grid Properties:**

*   `grid-template-columns`, `grid-template-rows`: Define the size and number of columns/rows.
*   `grid-gap`, `row-gap`, `column-gap`: Space between grid items.
*   `grid-column`, `grid-row`: Position grid items.
*   `grid-template-areas`: Define named grid areas.

## When to Use Which

*   **Use Flexbox for:**
    *   One-dimensional layouts (single row or column).
    *   Distributing space between items.
    *   Aligning items within a container.
    *   Components like navigation bars, forms, or card layouts.

*   **Use CSS Grid for:**
    *   Two-dimensional layouts (rows and columns simultaneously).
    *   Overall page layouts (header, sidebar, main content, footer).
    *   Complex grid structures where items span multiple rows and columns.

## Code Examples

### Flexbox Example (Navigation Bar)

```html
<nav class="navbar">
  <a href="#">Home</a>
  <a href="#">About</a>
  <a href="#">Services</a>
  <a href="#">Contact</a>
</nav>

<style>
  .navbar {
    display: flex;
    justify-content: space-around;
    align-items: center;
    background-color: #333;
    padding: 10px;
  }
  .navbar a {
    color: white;
    text-decoration: none;
    padding: 5px 10px;
  }
</style>
```

### CSS Grid Example (Page Layout)

```html
<div class="grid-container">
  <header class="header">Header</header>
  <aside class="sidebar">Sidebar</aside>
  <main class="main">Main Content</main>
  <footer class="footer">Footer</footer>
</div>

<style>
  .grid-container {
    display: grid;
    grid-template-columns: 1fr 3fr;
    grid-template-rows: auto 1fr auto;
    grid-template-areas:
      "header header"
      "sidebar main"
      "footer footer";
    height: 100vh;
  }
  .header { grid-area: header; background-color: lightblue; }
  .sidebar { grid-area: sidebar; background-color: lightgreen; }
  .main { grid-area: main; background-color: lightcoral; }
  .footer { grid-area: footer; background-color: lightgray; }
</style>
```

## Resources

*   **Article:** [MDN - Basic concepts of flexbox](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox)
*   **Article:** [MDN - Basic concepts of grid layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Basic_Concepts_of_Grid_Layout)
*   **Guide:** [A Complete Guide to Flexbox - CSS-Tricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
*   **Guide:** [A Complete Guide to CSS Grid - CSS-Tricks](https://css-tricks.com/snippets/css/a-complete-guide-to-css-grid/)
*   **Video:** [Flexbox vs CSS Grid - Kevin Powell](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
