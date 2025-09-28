
# 8. CSS Transitions vs. Animations

## Quick Revision

Both **CSS Transitions** and **CSS Animations** allow you to create dynamic visual effects on web elements. However, they are designed for different use cases.

*   **Transitions:** Used for creating smooth changes between two states of an element (e.g., on hover, focus, or class change). They are typically triggered by a user interaction or a state change.

*   **Animations:** Used for creating more complex, multi-step, and often continuous visual effects. They are defined using `@keyframes` and can run automatically or be triggered.

## Detailed Explanation

### CSS Transitions

Transitions provide a way to animate changes in CSS properties over a specified duration. They are ideal for simple, single-state changes.

**Key Properties:**

*   **`transition-property`:** Specifies the CSS property to which the transition should be applied (e.g., `background-color`, `opacity`, `transform`). Use `all` to transition all properties.
*   **`transition-duration`:** Specifies how long the transition should take to complete (e.g., `0.5s`, `500ms`).
*   **`transition-timing-function`:** Specifies the speed curve of the transition (e.g., `ease`, `linear`, `ease-in-out`).
*   **`transition-delay`:** Specifies a delay before the transition starts.
*   **`transition` (shorthand):** Combines all transition properties into a single declaration.

### CSS Animations

Animations allow you to define a sequence of CSS styles that an element will cycle through. They are more powerful and flexible than transitions.

**Key Concepts:**

*   **`@keyframes`:** Defines the animation sequence. You specify styles at different points (percentages or `from`/`to`) in the animation.
*   **`animation-name`:** Specifies the name of the `@keyframes` rule to use.
*   **`animation-duration`:** Specifies how long the animation should take to complete.
*   **`animation-timing-function`:** Specifies the speed curve of the animation.
*   **`animation-delay`:** Specifies a delay before the animation starts.
*   **`animation-iteration-count`:** Specifies how many times the animation should play (e.g., `infinite`).
*   **`animation-direction`:** Specifies whether the animation should play forwards, backwards, or alternate.
*   **`animation-fill-mode`:** Specifies how a CSS animation should apply styles to its target before and after its execution.
*   **`animation` (shorthand):** Combines all animation properties into a single declaration.

## Code Examples

### CSS Transition Example

```html
<div class="box transition-box"></div>

<style>
  .transition-box {
    width: 100px;
    height: 100px;
    background-color: blue;
    transition: background-color 0.5s ease-in-out, transform 0.5s ease-in-out;
  }

  .transition-box:hover {
    background-color: red;
    transform: scale(1.2);
  }
</style>
```

### CSS Animation Example

```html
<div class="box animation-box"></div>

<style>
  @keyframes pulse {
    0% {
      transform: scale(1);
      opacity: 1;
    }
    50% {
      transform: scale(1.1);
      opacity: 0.7;
    }
    100% {
      transform: scale(1);
      opacity: 1;
    }
  }

  .animation-box {
    width: 100px;
    height: 100px;
    background-color: green;
    animation: pulse 2s infinite alternate;
  }
</style>
```

## Summary

| Feature      | Transitions                              | Animations                               |
|--------------|------------------------------------------|------------------------------------------|
| **Purpose**  | Smooth changes between two states        | Complex, multi-step visual effects       |
| **Trigger**  | State change (e.g., `:hover`, `:focus`)  | Can run automatically or be triggered    |
| **Control**  | Limited (start, end)                     | Fine-grained control with `@keyframes`   |
| **Complexity**| Simpler                                  | More complex                             |

## Resources

*   **Article:** [MDN - Using CSS transitions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions)
*   **Article:** [MDN - Using CSS animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations)
*   **Video:** [CSS Transitions vs Animations - Kevin Powell](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
