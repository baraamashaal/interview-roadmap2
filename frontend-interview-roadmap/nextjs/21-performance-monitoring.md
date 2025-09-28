
# 21. Performance Monitoring in Next.js

## Quick Revision

**Performance monitoring** in Next.js involves tracking and analyzing various metrics to ensure your application is fast and responsive. Next.js provides built-in tools and integrates well with third-party services to help you identify and resolve performance bottlenecks.

Key areas include:

*   **Web Vitals:** Core Web Vitals (LCP, FID, CLS) are crucial for user experience and SEO.
*   **`next/app` and `reportWebVitals`:** Built-in function to report Web Vitals.
*   **Third-party analytics:** Integrating with services like Google Analytics, Vercel Analytics, or custom solutions.

## Detailed Explanation

Monitoring the performance of your Next.js application is essential for maintaining a good user experience and achieving high search engine rankings.

### 1. Web Vitals

Google's **Core Web Vitals** are a set of metrics that measure the real-world user experience of loading performance, interactivity, and visual stability of a page.

*   **Largest Contentful Paint (LCP):** Measures loading performance. To provide a good user experience, LCP should occur within 2.5 seconds of when the page first starts loading.
*   **First Input Delay (FID):** Measures interactivity. To provide a good user experience, pages should have an FID of 100 milliseconds or less.
*   **Cumulative Layout Shift (CLS):** Measures visual stability. To provide a good user experience, pages should maintain a CLS of 0.1. or less.

### 2. `next/app` and `reportWebVitals`

Next.js provides a `reportWebVitals` function that you can use in your custom `pages/_app.js` file to send Web Vitals data to any analytics endpoint.

```jsx
// pages/_app.js
export function reportWebVitals(metric) {
  console.log(metric); // Log all Web Vitals metrics

  // Example: send to Google Analytics
  // const body = JSON.stringify(metric);
  // const url = 'https://example.com/analytics';
  // navigator.sendBeacon(url, body);
}

function MyApp({ Component, pageProps }) {
  return <Component {...pageProps} />;
}

export default MyApp;
```

### 3. Third-Party Analytics

Next.js integrates seamlessly with various analytics platforms:

*   **Google Analytics:** You can send Web Vitals data to Google Analytics using the `reportWebVitals` function.
*   **Vercel Analytics:** If you deploy your Next.js application to Vercel, you get built-in analytics that track page views, unique visitors, and Web Vitals.
*   **Custom Solutions:** You can send metrics to your own custom analytics backend.

### 4. Performance Auditing Tools

*   **Lighthouse:** An open-source, automated tool for improving the quality of web pages. It has audits for performance, accessibility, progressive web apps, and more.
*   **Chrome DevTools:** The **Performance** and **Network** tabs in Chrome DevTools are invaluable for identifying performance bottlenecks.

## Code Example

### Sending Web Vitals to a Custom Endpoint

```jsx
// pages/_app.js
export function reportWebVitals(metric) {
  const body = JSON.stringify(metric);
  // Replace with your actual analytics endpoint
  const url = 'https://your-analytics-backend.com/api/web-vitals';

  // Use navigator.sendBeacon for reliable sending of data
  // even if the user closes the page.
  navigator.sendBeacon(url, body);
}

function MyApp({ Component, pageProps }) {
  return <Component {...pageProps} />;
}

export default MyApp;
```

## Resources

*   **Article:** [Next.js Docs - Measuring performance](https://nextjs.org/docs/advanced-features/measuring-performance)
*   **Article:** [Google - Core Web Vitals](https://web.dev/vitals/)
*   **Tool:** [Lighthouse](https://developers.google.com/web/tools/lighthouse)
*   **Video:** [Next.js Performance Optimization - Fireship](https://www.youtube.com/watch?v=N5R6oX6bLpA)
