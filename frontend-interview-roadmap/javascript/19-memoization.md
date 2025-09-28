
# 19. Memoization in JavaScript

## Quick Revision

**Memoization** is an optimization technique used to speed up function calls by caching the results of expensive function calls and returning the cached result when the same inputs occur again. It's a way of trading memory for speed.

## Detailed Explanation

Memoization is particularly useful for functions that are "pure," meaning they will always produce the same output for the same input and have no side effects.

The basic idea is to store the results of previous function calls in a cache (usually an object or a `Map`). When the function is called again with the same arguments, it first checks if the result is already in the cache. If it is, it returns the cached result. If not, it computes the result, stores it in the cache, and then returns it.

### How to Implement Memoization

You can create a higher-order function that takes a function as an argument and returns a memoized version of that function.

```javascript
function memoize(fn) {
  const cache = {};

  return function(...args) {
    const key = JSON.stringify(args);

    if (cache[key]) {
      return cache[key];
    } else {
      const result = fn.apply(this, args);
      cache[key] = result;
      return result;
    }
  };
}
```

## Code Examples

### Memoizing a Fibonacci Function

The Fibonacci sequence is a classic example of a function that can be optimized with memoization.

```javascript
function fibonacci(n) {
  if (n <= 1) {
    return n;
  }
  return fibonacci(n - 1) + fibonacci(n - 2);
}

const memoizedFibonacci = memoize(fibonacci);

console.time('Fibonacci');
console.log(memoizedFibonacci(40));
console.timeEnd('Fibonacci');

console.time('Fibonacci again');
console.log(memoizedFibonacci(40));
console.timeEnd('Fibonacci again');
```

The first time `memoizedFibonacci(40)` is called, it will be slow. The second time, it will be almost instantaneous because the result is retrieved from the cache.

## Use Cases

*   **Expensive computations:** Any function that performs a lot of calculations and is called repeatedly with the same arguments.
*   **Recursive functions:** Memoization can be used to optimize recursive functions by caching the results of subproblems.
*   **API calls:** You can memoize the results of API calls to avoid making unnecessary requests for the same data.

## Resources

*   **Article:** [Understanding Memoization in JavaScript](https://www.freecodecamp.org/news/understanding-memoize-in-javascript-51d07d19430e/)
*   **Article:** [MDN - Memoization](https://developer.mozilla.org/en-US/docs/Glossary/Memoization)
*   **Video:** [Memoization - Beau teaches JavaScript](https://www.youtube.com/watch?v=W-A_y_G-Y_Q)
