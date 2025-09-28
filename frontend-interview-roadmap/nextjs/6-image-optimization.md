
# 6. Image Optimization in Next.js

## Quick Revision

**Image optimization** is crucial for web performance. Next.js provides a built-in **`next/image`** component that automatically optimizes images for you. It handles responsive sizing, lazy loading, and modern image formats like WebP.

## Detailed Explanation

Images often account for a significant portion of a web page's total size, directly impacting load times and user experience. Next.js's `Image` component is designed to address these performance concerns out-of-the-box.

### The `next/image` Component

The `next/image` component is an extension of the HTML `<img>` tag with several built-in optimizations:

1.  **Automatic Image Optimization:**
    *   **Resizing:** Images are automatically resized to fit the viewport, serving smaller images for smaller screens.
    *   **Format Optimization:** Images are converted to modern formats like WebP when supported by the browser, which can significantly reduce file size.
    *   **Quality Optimization:** Images are compressed to reduce file size without a noticeable loss in quality.

2.  **Lazy Loading:** Images are lazy-loaded by default. This means images outside the viewport are not loaded until the user scrolls near them, saving bandwidth and improving initial page load time.

3.  **Layout Shift Prevention:** The `Image` component helps prevent Cumulative Layout Shift (CLS) by reserving space for the image before it loads, reducing jarring layout changes.

4.  **Domain Configuration:** For external images, you need to configure the `domains` property in `next.config.js` for security reasons.

### Required Props

*   **`src`:** The path to your image file (can be local or external).
*   **`width` and `height`:** Required for static images to prevent layout shift. For responsive images, you can use `layout="fill"`.
*   **`alt`:** Alternative text for the image, important for accessibility.

## Code Examples

### Local Image

```jsx
import Image from 'next/image';
import profilePic from '../public/profile.jpg';

function HomePage() {
  return (
    <Image
      src={profilePic}
      alt="Picture of the author"
      width={500} // Desired width in pixels
      height={500} // Desired height in pixels
    />
  );
}

export default HomePage;
```

### External Image

For external images, you need to configure `next.config.js`:

```javascript
// next.config.js
module.exports = {
  images: {
    domains: ['example.com', 'anotherdomain.com'],
  },
};
```

Then, in your component:

```jsx
import Image from 'next/image';

function MyImage() {
  return (
    <Image
      src="https://example.com/my-image.jpg"
      alt="Description of external image"
      width={600}
      height={400}
    />
  );
}

export default MyImage;
```

### Responsive Image (`layout="fill"`)

```jsx
import Image from 'next/image';

function ResponsiveImage() {
  return (
    <div style={{ position: 'relative', width: '100%', height: '300px' }}>
      <Image
        src="/my-responsive-image.jpg"
        alt="Responsive image"
        layout="fill"
        objectFit="cover"
      />
    </div>
  );
}

export default ResponsiveImage;
```

## Resources

*   **Article:** [Next.js Docs - Image Optimization](https://nextjs.org/docs/basic-features/image-optimization)
*   **Video:** [Next.js Image Component - Fireship](https://www.youtube.com/watch?v=S_K1_2_200Q)
