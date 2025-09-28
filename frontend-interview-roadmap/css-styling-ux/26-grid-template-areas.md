
# 26. `grid-template-areas` in CSS Grid

## Quick Revision

**`grid-template-areas`** is a powerful CSS Grid property that allows you to define the layout of your grid by naming grid areas and then arranging them visually. It provides a highly intuitive and readable way to design complex two-dimensional layouts.

## Detailed Explanation

Instead of relying on line numbers or explicit placement for grid items, `grid-template-areas` lets you draw your layout directly in CSS using strings. Each string represents a row in the grid, and the words within the string represent the named grid areas.

### How it Works

1.  **Define Grid Areas:** In the grid container, use `grid-template-areas` to define the layout. Each string represents a row, and each word in the string represents a named grid area. Identical names create a single, merged area.

    ```css
    .grid-container {
      display: grid;
      grid-template-columns: 1fr 2fr 1fr;
      grid-template-rows: auto 1fr auto;
      grid-template-areas:
        "header header header"
        "nav    main   aside"
        "footer footer footer";
    }
    ```

2.  **Assign Items to Areas:** In the grid items, use the `grid-area` property to assign them to the named areas.

    ```css
    .header { grid-area: header; }
    .nav { grid-area: nav; }
    .main { grid-area: main; }
    .aside { grid-area: aside; }
    .footer { grid-area: footer; }
    ```

### Benefits

*   **Readability:** The layout is visually represented in the CSS, making it very easy to understand the structure of the page.
*   **Maintainability:** Changes to the layout can be made by simply editing the `grid-template-areas` property, without touching individual grid item placements.
*   **Responsiveness:** Easily change the layout for different screen sizes by redefining `grid-template-areas` within media queries.

### Considerations

*   **Rectangular Areas:** Named grid areas must form a complete rectangle. You cannot create L-shaped or other irregular areas.
*   **Empty Cells:** Use a period (`.`) to represent an empty grid cell.

## Code Example

### Responsive Page Layout

```html
<div class="page-layout">
  <header class="page-header">Header</header>
  <nav class="page-nav">Navigation</nav>
  <main class="page-main">Main Content</main>
  <aside class="page-aside">Sidebar</aside>
  <footer class="page-footer">Footer</footer>
</div>

<style>
  .page-layout {
    display: grid;
    gap: 10px;
    min-height: 100vh;
    background-color: #f0f0f0;
    padding: 10px;

    /* Default layout for smaller screens (single column) */
    grid-template-columns: 1fr;
    grid-template-rows: auto 1fr auto auto auto;
    grid-template-areas:
      "header"
      "nav"
      "main"
      "aside"
      "footer";
  }

  .page-header { grid-area: header; background-color: lightcoral; padding: 20px; }
  .page-nav { grid-area: nav; background-color: lightblue; padding: 20px; }
  .page-main { grid-area: main; background-color: lightgreen; padding: 20px; }
  .page-aside { grid-area: aside; background-color: lightgoldenrodyellow; padding: 20px; }
  .page-footer { grid-area: footer; background-color: lightgray; padding: 20px; }

  /* Medium screens (e.g., tablets) */
  @media (min-width: 768px) {
    .page-layout {
      grid-template-columns: 1fr 3fr;
      grid-template-rows: auto 1fr auto;
      grid-template-areas:
        "header header"
        "nav    main"
        "aside  main"
        "footer footer";
    }
  }

  /* Large screens (e.g., desktops) */
  @media (min-width: 1024px) {
    .page-layout {
      grid-template-columns: 200px 1fr 250px;
      grid-template-rows: auto 1fr auto;
      grid-template-areas:
        "header header header"
        "nav    main   aside"
        "footer footer footer";
    }
  }
</style>
```

## Resources

*   **Article:** [MDN - `grid-template-areas`](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-areas)
*   **Article:** [CSS-Tricks - A Complete Guide to CSS Grid](https://css-tricks.com/snippets/css/a-complete-guide-to-css-grid/#aa-grid-template-areas)
*   **Video:** [CSS Grid Layout with `grid-template-areas` - Kevin Powell](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
