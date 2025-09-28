
# 9. Media Queries in CSS

## Quick Revision

**Media queries** are a CSS feature that allows you to apply styles selectively based on the characteristics of the device or viewport (e.g., screen width, height, orientation, resolution). They are a fundamental building block of **responsive web design**, enabling websites to adapt their layout and appearance to different screen sizes.

## Detailed Explanation

Media queries consist of a media type (e.g., `screen`, `print`) and one or more media features (e.g., `min-width`, `max-height`). If the media type and all media features are true, the styles inside the media query block are applied.

### Syntax

```css
@media media_type and (media_feature) {
  /* CSS rules to apply */
}
```

*   **`media_type`:** Specifies the type of device the media query applies to. Common types include:
    *   `all`: For all media types.
    *   `print`: For paged material and documents viewed on a screen in print preview mode.
    *   `screen`: For computer screens, tablets, and smartphones.
*   **`media_feature`:** Describes specific characteristics of the media. Common features include:
    *   `width`, `min-width`, `max-width`: Viewport width.
    *   `height`, `min-height`, `max-height`: Viewport height.
    *   `orientation`: `portrait` or `landscape`.
    *   `resolution`: Pixel density of the screen.

### Common Media Query Usage

1.  **Breakpoints:** Defining specific screen widths at which the layout changes.

    ```css
    /* Small devices (phones, 600px and down) */
    @media only screen and (max-width: 600px) {
      body { background-color: lightblue; }
    }

    /* Medium devices (tablets, 601px and up) */
    @media only screen and (min-width: 601px) {
      body { background-color: lightgreen; }
    }

    /* Large devices (desktops, 768px and up) */
    @media only screen and (min-width: 768px) {
      body { background-color: lightcoral; }
    }
    ```

2.  **Mobile-First Approach:** It's generally recommended to design for mobile devices first and then use `min-width` media queries to add styles for larger screens.

    ```css
    /* Default styles for mobile */
    .container { width: 100%; }

    @media (min-width: 768px) {
      .container { width: 750px; }
    }

    @media (min-width: 992px) {
      .container { width: 970px; }
    }
    ```

### Logical Operators

Media queries can be combined using logical operators:

*   **`and`:** Combines multiple media features.
*   **`not`:** Negates a media query.
*   **`,` (comma):** Acts as an `or` operator, applying styles if any of the queries are true.

## Code Examples

### Responsive Navigation Bar

```html
<nav class="navbar">
  <ul class="nav-list">
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Services</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>

<style>
  .nav-list {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex;
    flex-direction: column; /* Default to column for mobile */
  }
  .nav-list li a {
    display: block;
    padding: 10px;
    text-decoration: none;
    color: black;
    border-bottom: 1px solid #eee;
  }

  @media (min-width: 768px) {
    .nav-list {
      flex-direction: row; /* Row for larger screens */
      justify-content: space-around;
    }
    .nav-list li a {
      border-bottom: none;
    }
  }
</style>
```

### Orientation-based Styling

```css
@media (orientation: landscape) {
  body {
    background-color: #f0f8ff; /* AliceBlue in landscape */
  }
}

@media (orientation: portrait) {
  body {
    background-color: #fff0f5; /* LavenderBlush in portrait */
  }
}
```

## Resources

*   **Article:** [MDN - Media queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries)
*   **Article:** [CSS-Tricks - Media Queries for Standard Devices](https://css-tricks.com/snippets/css/media-queries-for-standard-devices/)
*   **Video:** [Media Queries Explained - Kevin Powell](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
