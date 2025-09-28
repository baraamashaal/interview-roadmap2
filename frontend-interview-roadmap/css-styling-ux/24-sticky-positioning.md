
# 24. Sticky Positioning in CSS

## Quick Revision

**`position: sticky`** is a CSS positioning value that allows an element to behave like `position: relative` until it reaches a specified scroll position (threshold), at which point it becomes `position: fixed`. This creates a "sticky" effect, commonly used for navigation bars, table headers, or sidebars that stick to the top of the viewport when scrolled past.

## Detailed Explanation

`position: sticky` is a hybrid of `relative` and `fixed` positioning. It allows an element to remain in the normal document flow until a certain scroll offset is met within its nearest scrolling ancestor (or the viewport if no scrolling ancestor is found).

### How `position: sticky` Works

1.  **Normal Flow:** Initially, the element behaves like a `position: relative` element, occupying its space in the document flow.
2.  **Scroll Threshold:** When the user scrolls and the element's position (relative to the viewport) crosses a defined threshold (specified by `top`, `right`, `bottom`, or `left`), it becomes "stuck."
3.  **Fixed Behavior:** Once stuck, it behaves like `position: fixed`, remaining in place relative to the viewport until its parent container scrolls out of view.

### Key Requirements

*   **`top`, `right`, `bottom`, or `left`:** At least one of these offset properties **must** be specified for `position: sticky` to work. Without them, the element will behave as if it has `position: relative`.
*   **Scrolling Ancestor:** The sticky element needs a scrolling ancestor (or the viewport itself) to calculate its stickiness. If the parent element is not scrollable, the sticky effect might not work as expected.
*   **Overflow:** The parent container of the sticky element must not have `overflow: hidden`, `overflow: scroll`, or `overflow: auto` set on it, as this can prevent the sticky behavior.

## Code Example

### Sticky Header

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sticky Header Example</title>
  <style>
    body {
      margin: 0;
      font-family: sans-serif;
      height: 2000px; /* To enable scrolling */
      background: linear-gradient(to bottom, #f0f0f0, #ccc);
    }

    .header {
      background-color: #333;
      color: white;
      padding: 15px;
      text-align: center;
      position: sticky;
      top: 0; /* This makes it sticky to the top of the viewport */
      z-index: 1000;
      box-shadow: 0 2px 5px rgba(0,0,0,0.2);
    }

    .content {
      padding: 20px;
      margin-top: 20px;
    }

    .section {
      height: 400px;
      background-color: #fff;
      margin-bottom: 20px;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 1px 3px rgba(0,0,0,0.1);
    }
  </style>
</head>
<body>

  <header class="header">
    <h1>My Sticky Header</h1>
  </header>

  <div class="content">
    <div class="section">Section 1: Scroll down to see the header stick.</div>
    <div class="section">Section 2: More content here.</div>
    <div class="section">Section 3: Keep scrolling!</div>
  </div>

</body>
</html>
```

### Sticky Sidebar

```html
<div class="main-layout">
  <aside class="sidebar">
    <h3>Sticky Sidebar</h3>
    <ul>
      <li>Item 1</li>
      <li>Item 2</li>
      <li>Item 3</li>
    </ul>
  </aside>
  <main class="main-content">
    <p>Long content to enable scrolling...</p>
    <!-- Add a lot of content here to make the page scrollable -->
    <div style="height: 1500px;"></div>
  </main>
</div>

<style>
  .main-layout {
    display: flex;
    gap: 20px;
    padding: 20px;
  }
  .sidebar {
    width: 200px;
    background-color: #e0f7fa;
    padding: 15px;
    border-radius: 8px;
    position: sticky;
    top: 20px; /* Sticks 20px from the top of the viewport */
    align-self: flex-start; /* Important for sticky in flex containers */
    height: fit-content; /* Prevents sidebar from taking full height */
  }
  .main-content {
    flex-grow: 1;
    background-color: #fff;
    padding: 20px;
    border-radius: 8px;
  }
</style>
```

## Resources

*   **Article:** [MDN - `position: sticky`](https://developer.mozilla.org/en-US/docs/Web/CSS/position#sticky)
*   **Article:** [CSS-Tricks - `position: sticky` Explained](https://css-tricks.com/position-sticky-explained/)
*   **Video:** [CSS `position: sticky` - Kevin Powell](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
