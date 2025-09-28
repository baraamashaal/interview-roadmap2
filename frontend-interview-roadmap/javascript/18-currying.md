
# 18. Currying in JavaScript

## Quick Revision

**Currying** is a functional programming technique that transforms a function with multiple arguments into a sequence of nested functions, each taking a single argument. Instead of taking all arguments at once, the curried function takes the first argument and returns a new function that takes the second argument, and so on, until all arguments have been supplied.

## Detailed Explanation

Currying allows you to create more specialized and reusable functions. It can be used to:

*   **Create specialized functions:** You can create a new function by partially applying arguments to a curried function.
*   **Improve code readability:** Currying can make your code more declarative and easier to read.
*   **Compose functions:** Currying is a key concept in function composition.

### How to Implement Currying

You can implement currying in JavaScript using closures.

```javascript
function curry(fn) {
  return function curried(...args) {
    if (args.length >= fn.length) {
      return fn.apply(this, args);
    } else {
      return function(...args2) {
        return curried.apply(this, args.concat(args2));
      };
    }
  };
}
```

This `curry` function takes a function `fn` as an argument and returns a new curried function. The curried function checks if it has received all the arguments it needs. If it has, it calls the original function. If not, it returns a new function that waits for the remaining arguments.

## Code Examples

### Basic Currying Example

```javascript
function add(a, b, c) {
  return a + b + c;
}

const curriedAdd = curry(add);

const add5 = curriedAdd(5);
const add5and10 = add5(10);

console.log(add5and10(15)); // 30
console.log(curriedAdd(5)(10)(15)); // 30
```

### Practical Use Case: Logging

```javascript
function log(level, message) {
  console.log(`[${level}] ${message}`);
}

const curriedLog = curry(log);

const infoLog = curriedLog('INFO');
const errorLog = curriedLog('ERROR');

infoLog('This is an informational message.');
errorLog('This is an error message.');
```

## Resources

*   **Article:** [JavaScript Currying for Beginners](https://www.freecodecamp.org/news/javascript-currying-for-beginners/)
*   **Article:** [Currying in JavaScript](https://javascript.info/currying-partials)
*   **Video:** [Currying - Beau teaches JavaScript](https://www.youtube.com/watch?v=iZLP4qOwY8I)
