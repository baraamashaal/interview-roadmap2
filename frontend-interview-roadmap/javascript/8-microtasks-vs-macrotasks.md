
# 8. Microtasks vs. Macrotasks in JavaScript

## Quick Revision

The **Event Loop** has two types of queues for asynchronous tasks: the **Microtask Queue** and the **Macrotask Queue** (also known as the Task Queue).

*   **Macrotasks:** Include tasks like `setTimeout`, `setInterval`, `setImmediate`, I/O operations, and UI rendering.
*   **Microtasks:** Include tasks like `Promise.then()`, `Promise.catch()`, `Promise.finally()`, `async/await`, and `MutationObserver`.

The Event Loop has a specific order of execution: it executes one macrotask, then it executes **all** available microtasks, then it proceeds to the next macrotask.

## Detailed Explanation

To understand the difference between microtasks and macrotasks, it's important to have a good grasp of the Event Loop.

### The Event Loop Process

1.  **Dequeue and execute a macrotask:** The Event Loop takes the oldest task from the Macrotask Queue and executes it.
2.  **Execute all microtasks:** After the macrotask is finished, the Event Loop processes the Microtask Queue. It executes all microtasks in the queue, one by one, until the queue is empty. If a microtask adds another microtask to the queue, that new microtask will also be executed before the Event Loop continues.
3.  **Render the UI (if applicable):** The browser may then update the rendering.
4.  **Repeat:** The Event Loop then returns to step 1 to process the next macrotask.

### Key Differences

*   **Priority:** Microtasks have a higher priority than macrotasks. The Microtask Queue is always processed before the next macrotask.
*   **Execution:** All available microtasks are executed in a single go, while only one macrotask is executed at a time.

## Code Example

```javascript
console.log('1. Script start');

setTimeout(() => {
  console.log('4. setTimeout (macrotask)');
}, 0);

Promise.resolve().then(() => {
  console.log('3. Promise (microtask)');
});

console.log('2. Script end');
```

**Execution Order:**

1.  `console.log('1. Script start')` is executed.
2.  `setTimeout()` is a macrotask, so its callback is placed in the Macrotask Queue.
3.  `Promise.resolve().then()` is a microtask, so its callback is placed in the Microtask Queue.
4.  `console.log('2. Script end')` is executed.
5.  The main script (which is a macrotask) is finished. The Event Loop now checks the Microtask Queue.
6.  The `Promise` callback is executed, and `console.log('3. Promise (microtask)')` is printed.
7.  The Microtask Queue is now empty. The Event Loop checks the Macrotask Queue.
8.  The `setTimeout` callback is executed, and `console.log('4. setTimeout (macrotask)')` is printed.

**Output:**

```
1. Script start
2. Script end
3. Promise (microtask)
4. setTimeout (macrotask)
```

## Another Example

```javascript
Promise.resolve().then(() => console.log('Promise 1'));
setTimeout(() => console.log('setTimeout 1'), 0);

Promise.resolve().then(() => {
  console.log('Promise 2');
  setTimeout(() => console.log('setTimeout 2'), 0);
});

Promise.resolve().then(() => console.log('Promise 3'));
```

**Output:**

```
Promise 1
Promise 2
Promise 3
setTimeout 1
setTimeout 2
```

## Resources

*   **Video:** [In The Loop - Jake Archibald | JSConf.Asia](https://www.youtube.com/watch?v=cCOL7MC4Pl0)
*   **Article:** [MDN - Using microtasks in JavaScript](https://developer.mozilla.org/en-US/docs/Web/API/HTML_DOM_API/Microtask_guide)
*   **Article:** [Tasks, Microtasks, Queues, and Schedules](https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/)
