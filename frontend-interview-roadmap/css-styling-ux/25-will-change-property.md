
# 25. `will-change` Property in CSS

## Quick Revision

The **`will-change`** CSS property allows you to inform the browser ahead of time of what kinds of changes you expect to make to an element. This allows the browser to optimize for those changes before they actually happen, potentially improving performance by preparing for animations or transitions.

## Detailed Explanation

When an element is animated or transitioned, the browser often has to perform complex calculations (layout, paint, composite) on the fly. This can sometimes lead to jank or stuttering, especially on less powerful devices or with complex animations.

The `will-change` property is a performance hint to the browser. By telling the browser which properties are likely to change, it can make optimizations (like creating a new rendering layer for the element) in advance, avoiding the performance hit when the change actually occurs.

### How it Works

When you apply `will-change` to an element, the browser might:

*   **Promote the element to its own layer:** This allows the browser to animate the element without affecting other elements on the page, reducing repaints.
*   **Allocate more memory:** For the element, to store its current state and prepare for future changes.

### Values

*   **`auto`:** Default value. No specific optimizations are made.
*   **`<custom-ident>`:** A list of one or more CSS properties that are expected to change (e.g., `transform`, `opacity`, `left`, `top`).
*   **`scroll-position`:** Indicates that the element's scroll position is expected to change.
*   **`contents`:** Indicates that the element's content is expected to change.

### Best Practices

*   **Use sparingly:** `will-change` can consume significant resources. Only use it on elements that are actually going to change, and remove it when the change is complete.
*   **Don't apply to too many elements:** Overuse can lead to performance degradation rather than improvement.
*   **Apply just before the change:** Apply `will-change` just before the animation or transition starts, and remove it when it finishes.

## Code Examples

### Optimizing an Animation with `will-change`

```html
<div class="box">
  Hover over me
</div>

<style>
  .box {
    width: 100px;
    height: 100px;
    background-color: blue;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: transform 0.3s ease-out, background-color 0.3s ease-out;
    /* Inform the browser that transform and background-color will change */
    will-change: transform, background-color;
  }

  .box:hover {
    transform: scale(1.2) rotate(10deg);
    background-color: red;
  }
</style>
```

### Using `will-change` with JavaScript

```html
<button id="animateButton">Animate</button>
<div id="animatedBox" class="box"></div>

<style>
  .box {
    width: 100px;
    height: 100px;
    background-color: green;
    margin-top: 20px;
    transition: transform 0.5s ease-out;
  }

  .box.is-animating {
    transform: translateX(100px) scale(1.5);
  }
</style>

<script>
  const animateButton = document.getElementById('animateButton');
  const animatedBox = document.getElementById('animatedBox');

  animateButton.addEventListener('click', () => {
    // Add will-change just before the animation starts
    animatedBox.style.willChange = 'transform';
    animatedBox.classList.add('is-animating');

    // Remove will-change after the animation finishes
    animatedBox.addEventListener('transitionend', () => {
      animatedBox.style.willChange = 'auto';
    }, { once: true });
  });
</script>
```

## Resources

*   **Article:** [MDN - `will-change`](https://developer.mozilla.org/en-US/docs/Web/CSS/will-change)
*   **Article:** [CSS-Tricks - The `will-change` Property](https://css-tricks.com/almanac/properties/w/will-change/)
*   **Video:** [CSS `will-change` Explained - Google Chrome Developers](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
