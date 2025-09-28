
# 1. Explain the Event Loop and Call Stack in JavaScript

## Quick Revision

The **Call Stack** is a data structure that tracks the execution of functions in a Last-In, First-Out (LIFO) order. When a function is called, it's pushed onto the stack, and when it returns, it's popped off.

The **Event Loop** is a mechanism that enables non-blocking asynchronous operations in JavaScript, a single-threaded language. It continuously checks the **Call Stack** and the **Callback Queue**. If the Call Stack is empty, it takes the first event from the Callback Queue and pushes it onto the Call Stack for execution.

## Detailed Explanation

JavaScript is a single-threaded language, meaning it can only execute one task at a time. This is where the Call Stack comes in. It's a simple data structure that keeps track of the currently executing function.

**The Call Stack:**

*   When a script is executed, the global execution context is pushed onto the stack.
*   When a function is called, a new execution context for that function is created and pushed onto the top of the stack.
*   When the function finishes, its execution context is popped off the stack.
*   If the stack is full (e.g., due to infinite recursion), a "stack overflow" error occurs.

**The Callback Queue (or Task Queue):**

Asynchronous operations (like `setTimeout`, AJAX requests, or DOM events) are handled by Web APIs provided by the browser. When an asynchronous task is complete, its callback function is not immediately executed. Instead, it's placed in the Callback Queue.

**The Event Loop:**

The Event Loop's job is to monitor the Call Stack and the Callback Queue.

1.  It waits for the Call Stack to be empty.
2.  Once the Call Stack is empty, it checks the Callback Queue.
3.  If there are any functions in the Callback Queue, it dequeues the first one and pushes it onto the Call Stack.
4.  The Call Stack then executes the function.

This process repeats continuously, allowing JavaScript to handle asynchronous operations without blocking the main thread.

### Microtasks and Macrotasks

The Callback Queue is further divided into two queues:

*   **Macrotask Queue (or Task Queue):**  For tasks like `setTimeout`, `setInterval`, `setImmediate`, and I/O operations.
*   **Microtask Queue:** For tasks like `Promise.then()`, `Promise.catch()`, `Promise.finally()`, `async/await`, and `MutationObserver`.

The Event Loop prioritizes the Microtask Queue. After each macrotask is completed, the Event Loop processes **all** microtasks in the Microtask Queue before moving on to the next macrotask.

## Code Examples

### Call Stack Example

```javascript
function first() {
  console.log('First function');
  second();
  console.log('First function again');
}

function second() {
  console.log('Second function');
  third();
  console.log('Second function again');
}

function third() {
  console.log('Third function');
}

first();
```

**Execution Order:**

1.  `first()` is called and pushed to the stack.
2.  `console.log('First function')` is executed.
3.  `second()` is called and pushed to the stack.
4.  `console.log('Second function')` is executed.
5.  `third()` is called and pushed to the stack.
6.  `console.log('Third function')` is executed.
7.  `third()` returns and is popped from the stack.
8.  `console.log('Second function again')` is executed.
9.  `second()` returns and is popped from the stack.
10. `console.log('First function again')` is executed.
11. `first()` returns and is popped from the stack.

### Event Loop Example

```javascript
console.log('Start');

setTimeout(() => {
  console.log('setTimeout callback');
}, 0);

Promise.resolve().then(() => {
  console.log('Promise resolved');
});

console.log('End');
```

**Execution Order:**

1.  `console.log('Start')` is executed.
2.  `setTimeout()` is a Web API, so its callback is sent to the Macrotask Queue.
3.  `Promise.resolve().then()` is a microtask, so its callback is sent to the Microtask Queue.
4.  `console.log('End')` is executed.
5.  The Call Stack is now empty. The Event Loop checks the Microtask Queue first.
6.  The `Promise` callback is moved to the Call Stack and `console.log('Promise resolved')` is executed.
7.  The Microtask Queue is now empty. The Event Loop checks the Macrotask Queue.
8.  The `setTimeout` callback is moved to the Call Stack and `console.log('setTimeout callback')` is executed.

**Output:**

```
Start
End
Promise resolved
setTimeout callback
```

## Resources

*   **Video:** [What the heck is the event loop anyway? | Philip Roberts | JSConf EU](https://www.youtube.com/watch?v=8aGhZQkoFbQ)
*   **Article:** [MDN - The Event Loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)
*   **Interactive Visualization:** [latentflip.com/loupe](http://latentflip.com/loupe/)
*   **Course:** [JavaScript: The Hard Parts, v2](https://frontendmasters.com/courses/javascript-hard-parts-v2/)
