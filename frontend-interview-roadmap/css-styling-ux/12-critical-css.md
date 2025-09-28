
# 12. Critical CSS

## Quick Revision

**Critical CSS** (or Critical Path CSS) is a performance optimization technique that involves extracting the minimum amount of CSS required to render the visible portion of a web page (the "above-the-fold" content) and inlining it directly into the HTML document's `<head>`. The rest of the CSS is then loaded asynchronously.

This technique aims to improve the **First Contentful Paint (FCP)** and **Largest Contentful Paint (LCP)** metrics, leading to a faster perceived load time and better user experience.

## Detailed Explanation

When a browser loads a web page, it encounters the HTML, then requests any linked CSS files. Until the CSS is downloaded and parsed, the browser cannot render the page, leading to a blank screen or unstyled content (Flash of Unstyled Content - FOUC).

Critical CSS addresses this by ensuring that the styles needed for the initial view are immediately available.

### How Critical CSS Works

1.  **Identify Critical Styles:** Tools analyze your page to determine which CSS rules are necessary to render the content visible in the initial viewport.
2.  **Extract and Inline:** These critical styles are extracted and inlined directly into a `<style>` tag within the `<head>` of your HTML document.
3.  **Asynchronous Loading:** The remaining, non-critical CSS is then loaded asynchronously (e.g., using `rel="preload"` with `onload` or JavaScript).

### Benefits

*   **Faster Perceived Performance:** The user sees content much faster, as the browser doesn't have to wait for external stylesheets.
*   **Improved Core Web Vitals:** Directly impacts FCP and LCP, which are important for SEO.
*   **Better User Experience:** Reduces the time users spend looking at a blank or unstyled page.

### Challenges

*   **Complexity:** Identifying critical CSS can be complex, especially for dynamic pages or single-page applications.
*   **Maintenance:** Critical CSS needs to be re-generated whenever the above-the-fold content or styles change.
*   **Tooling:** Requires build-time tooling to automate the extraction process.

## Code Example (Conceptual)

### Before Critical CSS

```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="/styles/main.css">
</head>
<body>
  <div id="app"></div>
</body>
</html>
```

### After Critical CSS

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Critical CSS for above-the-fold content */
    body { font-family: sans-serif; margin: 0; }
    .header { background-color: #333; color: white; padding: 1em; }
    /* ... more critical styles ... */
  </style>
  <link rel="preload" href="/styles/main.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
  <noscript><link rel="stylesheet" href="/styles/main.css"></noscript>
</head>
<body>
  <div id="app"></div>
</body>
</html>
```

In this example, the essential styles are inlined, allowing the browser to render the initial view immediately. The full `main.css` is preloaded and then applied once downloaded, ensuring a smooth transition.

## Tools for Critical CSS

*   **`critical` (NPM package):** A popular tool for extracting critical CSS.
*   **`critters` (Webpack plugin):** Integrates critical CSS generation into your Webpack build process.
*   **Next.js:** Can be configured to use these tools in its build process.

## Resources

*   **Article:** [Google - Optimize Critical Rendering Path](https://developers.google.com/speed/docs/insights/OptimizeCSSDelivery)
*   **Article:** [Critical CSS: What It Is & How To Use It](https://www.smashingmagazine.com/2015/08/understanding-critical-css/)
*   **Video:** [Critical CSS Explained - Google Chrome Developers](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
