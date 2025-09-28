
# 12. Debouncing vs. Throttling in JavaScript

## Quick Revision

**Debouncing** and **throttling** are two techniques used to control how often a function is executed. They are particularly useful for performance optimization with events that can fire rapidly, such as resizing the window, scrolling, or typing in an input field.

*   **Debouncing:** Groups a sequence of calls to a function into a single call. The function is only executed after a certain amount of time has passed without any new calls.

*   **Throttling:** Ensures that a function is executed at most once every specified period of time.

## Detailed Explanation

### Debouncing

Imagine you are in an elevator. When you press a floor button, the doors don't close immediately. Instead, the elevator waits for a few seconds to see if anyone else wants to press a button. Each new button press resets the timer. The elevator only moves after the timer has finished without any new button presses. This is debouncing.

**Use Cases for Debouncing:**

*   **Search input:** You don't want to send an API request for every keystroke. Instead, you can wait until the user has stopped typing.
*   **Window resizing:** You only want to recalculate the layout after the user has finished resizing the window.

### Throttling

Throttling is like a leaky bucket. No matter how much water you pour into it, the water only comes out at a constant rate.

**Use Cases for Throttling:**

*   **Scrolling:** You might want to update the UI based on the scroll position, but you don't need to do it for every single scroll event. Throttling can limit the updates to once every 100ms, for example.
*   **Button clicks:** Preventing a user from accidentally clicking a button multiple times in quick succession.

## Code Examples

### Debounce Implementation

```javascript
function debounce(func, delay) {
  let timeoutId;

  return function(...args) {
    clearTimeout(timeoutId);

    timeoutId = setTimeout(() => {
      func.apply(this, args);
    }, delay);
  };
}

// Example usage
const handleInput = (event) => {
  console.log('Searching for:', event.target.value);
};

const debouncedHandleInput = debounce(handleInput, 500);

document.getElementById('searchInput').addEventListener('input', debouncedHandleInput);
```

### Throttle Implementation

```javascript
function throttle(func, limit) {
  let inThrottle = false;

  return function(...args) {
    if (!inThrottle) {
      func.apply(this, args);
      inThrottle = true;
      setTimeout(() => {
        inThrottle = false;
      }, limit);
    }
  };
}

// Example usage
const handleScroll = () => {
  console.log('Scrolled!');
};

const throttledHandleScroll = throttle(handleScroll, 1000);

window.addEventListener('scroll', throttledHandleScroll);
```

## Resources

*   **Article:** [CSS-Tricks: Debouncing and Throttling Explained Through Examples](https://css-tricks.com/debouncing-throttling-explained-examples/)
*   **Video:** [Debounce and Throttle - Beau teaches JavaScript](https://www.youtube.com/watch?v=cjIswDCKgu0)
*   **Interactive Visualization:** [Debounce vs. Throttle](https://debouncing-throttling.netlify.app/)
*   **Library:** [Lodash `_.debounce()`](https://lodash.com/docs/4.17.15#debounce) and [`_.throttle()`](https://lodash.com/docs/4.17.15#throttle)
