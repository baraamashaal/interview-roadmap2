
# 7. Async/Await vs. Promises in JavaScript

## Quick Revision

**Promises** are objects that represent the eventual completion (or failure) of an asynchronous operation. They allow you to write asynchronous code in a more manageable way than traditional callbacks, but can still lead to complex chains of `.then()` calls.

**`async/await`**, introduced in ES2017, is syntactic sugar built on top of Promises. It allows you to write asynchronous code that looks and behaves more like synchronous code, making it easier to read and maintain.

## Detailed Explanation

### Promises

A `Promise` can be in one of three states:

*   **Pending:** The initial state; the operation has not completed yet.
*   **Fulfilled:** The operation completed successfully, and the promise has a resulting value.
*   **Rejected:** The operation failed, and the promise has a reason for the failure.

You can attach callbacks to a promise using the `.then()` and `.catch()` methods.

*   `.then(onFulfilled, onRejected)`: Takes two optional arguments, a callback for success and a callback for failure.
*   `.catch(onRejected)`: A shorthand for `.then(null, onRejected)`, used for handling errors.
*   `.finally(onFinally)`:  Called when the promise is settled (either fulfilled or rejected).

### `async/await`

`async/await` provides a more modern and readable syntax for working with Promises.

*   **`async` function:** The `async` keyword is used to declare an asynchronous function. An `async` function always returns a `Promise`. If the function returns a value, the `Promise` will be resolved with that value. If the function throws an exception, the `Promise` will be rejected with that exception.

*   **`await` operator:** The `await` keyword can only be used inside an `async` function. It pauses the execution of the function and waits for a `Promise` to be resolved. It then resumes the execution and returns the resolved value of the `Promise`.

### Key Differences

*   **Syntax:** `async/await` is more concise and readable, especially for complex asynchronous operations.
*   **Error Handling:** Error handling with `async/await` is done using standard `try...catch` blocks, which is more familiar to many developers than the `.catch()` method of Promises.
*   **Debugging:** `async/await` makes it easier to debug asynchronous code because you can step through the code as if it were synchronous.

## Code Examples

### Using Promises

```javascript
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const data = { message: 'Data fetched successfully!' };
      // resolve(data);
      reject(new Error('Failed to fetch data'));
    }, 1000);
  });
}

fetchData()
  .then(data => {
    console.log(data.message);
  })
  .catch(error => {
    console.error(error.message);
  })
  .finally(() => {
    console.log('Fetch operation finished.');
  });
```

### Using `async/await`

```javascript
async function fetchDataAsync() {
  try {
    const data = await fetchData();
    console.log(data.message);
  } catch (error) {
    console.error(error.message);
  } finally {
    console.log('Fetch operation finished.');
  }
}

fetchDataAsync();
```

As you can see, the `async/await` version is more linear and easier to follow.

## When to Use Which

*   `async/await` is generally preferred for writing asynchronous code in modern JavaScript due to its readability and ease of use.
*   Promises are still fundamental, and you will often use them directly when you need to work with APIs that return Promises or when you need to use methods like `Promise.all()`, `Promise.race()`, etc.

## Resources

*   **Article:** [MDN - async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
*   **Article:** [MDN - await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await)
*   **Article:** [JavaScript Promises for Dummies](https://www.freecodecamp.org/news/javascript-promises-for-dummies/)
*   **Video:** [Async/Await - Beau teaches JavaScript](https://www.youtube.com/watch?v=O_bSjsLga4U)
*   **Course:** [JavaScript: The Hard Parts, v2](https://frontendmasters.com/courses/javascript-hard-parts-v2/)
