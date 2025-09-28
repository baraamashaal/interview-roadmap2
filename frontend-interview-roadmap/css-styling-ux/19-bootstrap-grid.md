
# 19. Bootstrap Grid System

## Quick Revision

**Bootstrap's grid system** is a mobile-first, responsive layout system built with Flexbox. It allows you to create complex layouts by dividing the page into a series of rows and columns. The grid is based on a 12-column layout, providing a flexible and consistent way to arrange content across different screen sizes.

## Detailed Explanation

Bootstrap's grid system is one of its most powerful features, enabling developers to quickly build responsive and consistent layouts without writing extensive custom CSS.

### Key Concepts

1.  **Containers:** The outermost element that wraps your grid content. Bootstrap provides two types:
    *   **`.container`:** A fixed-width container that responds to breakpoints.
    *   **`.container-fluid`:** A full-width container that spans the entire viewport.

2.  **Rows:** Rows (`.row`) are wrappers for columns. They use negative margins to offset the padding of columns, ensuring proper alignment.

3.  **Columns:** Columns (`.col-*`) are the direct children of rows. They specify how much space an element should take up within a row. Bootstrap's grid is based on a 12-column system, so `col-6` would take up half the width of the row.

4.  **Breakpoints:** Bootstrap's grid is responsive and uses five default breakpoints to target different screen sizes:
    *   `xs` (extra small): < 576px (no prefix needed, e.g., `.col-6`)
    *   `sm` (small): ≥ 576px (e.g., `.col-sm-6`)
    *   `md` (medium): ≥ 768px (e.g., `.col-md-6`)
    *   `lg` (large): ≥ 992px (e.g., `.col-lg-6`)
    *   `xl` (extra large): ≥ 1200px (e.g., `.col-xl-6`)
    *   `xxl` (extra extra large): ≥ 1400px (e.g., `.col-xxl-6`)

### How it Works

*   **Flexbox-based:** The grid system leverages CSS Flexbox for its layout capabilities.
*   **Mobile-first:** Styles are applied to the smallest breakpoint first and then scale up to larger breakpoints.
*   **Gutters:** Columns have horizontal padding (gutters) to create space between content. Rows use negative margins to counteract this padding.

## Code Examples

### Basic Responsive Grid

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Bootstrap Grid Example</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
  <style>
    .col-content {
      background-color: #e9ecef;
      border: 1px solid #dee2e6;
      padding: 15px;
      text-align: center;
      margin-bottom: 10px;
    }
  </style>
</head>
<body>

  <div class="container">
    <div class="row">
      <div class="col-12 col-md-6 col-lg-4">
        <div class="col-content">Column 1</div>
      </div>
      <div class="col-12 col-md-6 col-lg-4">
        <div class="col-content">Column 2</div>
      </div>
      <div class="col-12 col-md-6 col-lg-4">
        <div class="col-content">Column 3</div>
      </div>
      <div class="col-12 col-md-6 col-lg-4">
        <div class="col-content">Column 4</div>
      </div>
    </div>
  </div>

</body>
</html>
```

**Explanation:**

*   On extra small screens (`<576px`), each column takes up the full width (`col-12`).
*   On medium screens (`≥576px`), columns take up half the width (`col-md-6`), resulting in two columns per row.
*   On large screens (`≥992px`), columns take up one-third the width (`col-lg-4`), resulting in three columns per row.

### Offsetting Columns

```html
<div class="container">
  <div class="row">
    <div class="col-md-4">
      <div class="col-content">.col-md-4</div>
    </div>
    <div class="col-md-4 offset-md-4">
      <div class="col-content">.col-md-4 .offset-md-4</div>
    </div>
  </div>
</div>
```

### Nesting Columns

```html
<div class="container">
  <div class="row">
    <div class="col-sm-9">
      <div class="col-content">Level 1: .col-sm-9</div>
      <div class="row">
        <div class="col-8 col-sm-6">
          <div class="col-content">Level 2: .col-8 .col-sm-6</div>
        </div>
        <div class="col-4 col-sm-6">
          <div class="col-content">Level 2: .col-4 .col-sm-6</div>
        </div>
      </div>
    </div>
  </div>
</div>
```

## Resources

*   **Official Docs:** [Bootstrap Grid System](https://getbootstrap.com/docs/5.3/layout/grid/)
*   **Video:** [Bootstrap 5 Grid System - Traversy Media](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
