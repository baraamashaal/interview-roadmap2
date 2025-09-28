
# 11. Memory Leaks in JavaScript: Causes and Fixes

## Quick Revision

**Memory leaks** in JavaScript occur when a program no longer needs a piece of memory but fails to release it. This can lead to a gradual decrease in available memory, eventually causing the application to slow down or crash. Common causes include:

*   **Accidental global variables**
*   **Closures that hold onto unnecessary variables**
*   **Detached DOM elements**
*   **Forgotten timers or callbacks**

## Detailed Explanation

JavaScript uses automatic memory management, primarily through a process called **garbage collection**. The garbage collector's job is to identify and free up memory that is no longer in use.

### How Garbage Collection Works

Most modern garbage collectors use a **mark-and-sweep** algorithm:

1.  The garbage collector starts from a set of "roots" (e.g., global variables, the current call stack).
2.  It "marks" all objects that are reachable from these roots.
3.  It "sweeps" away all unmarked objects, freeing up the memory they were using.

A memory leak occurs when an object is no longer needed by the application but is still reachable from a root. This prevents the garbage collector from reclaiming its memory.

### Common Causes of Memory Leaks

#### 1. Accidental Global Variables

If you forget to declare a variable with `let`, `const`, or `var`, it can become an accidental global variable. Global variables are never garbage collected.

```javascript
function createGlobal() {
  // Whoops, forgot to declare 'leaky'
  leaky = 'I am a global variable';
}
createGlobal();
```

**Fix:** Always declare your variables and use strict mode (`'use strict';`) to prevent this from happening silently.

#### 2. Closures

Closures can be a common source of memory leaks. An inner function can hold onto variables from its outer function, and if the inner function is kept alive, so are the outer function's variables.

```javascript
function outer() {
  const largeObject = new Array(1000000).fill('*');

  return function inner() {
    // This inner function has a closure over 'largeObject', even if it doesn't use it.
    return 'I am the inner function';
  };
}

const myInnerFunction = outer(); // 'largeObject' is still in memory
```

**Fix:** Be mindful of what variables are being captured in closures. If a variable is not needed, set it to `null` to break the reference.

#### 3. Detached DOM Elements

If you remove a DOM element from the page but still have a reference to it in your JavaScript code, it cannot be garbage collected.

```javascript
let detachedElement;

function createAndRemoveElement() {
  const element = document.createElement('div');
  document.body.appendChild(element);

  detachedElement = element; // Keep a reference to the element

  document.body.removeChild(element); // Remove the element from the DOM
}

createAndRemoveElement(); // 'detachedElement' still holds a reference to the removed element
```

**Fix:** Remove any references to detached DOM elements when they are no longer needed.

#### 4. Forgotten Timers or Callbacks

If you have a `setInterval` that is never cleared, it can keep its callback and any referenced variables alive indefinitely.

```javascript
function startTimer() {
  const data = { value: 'Some data' };

  setInterval(() => {
    // This callback keeps 'data' alive
    console.log(data.value);
  }, 1000);
}

startTimer();
```

**Fix:** Always clear your intervals and event listeners when they are no longer needed (e.g., in the `cleanup` function of a React `useEffect` hook).

## Tools for Detecting Memory Leaks

*   **Chrome DevTools:** The **Memory** and **Performance** panels in Chrome DevTools are powerful tools for analyzing memory usage, taking heap snapshots, and identifying memory leaks.

## Resources

*   **Article:** [MDN - Memory Management](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management)
*   **Article:** [4 Types of Memory Leaks in JavaScript and How to Get Rid Of Them](https://www.freecodecamp.org/news/4-types-of-memory-leaks-in-javascript-and-how-to-get-rid-of-them/)
*   **Video:** [Memory Leaks - Beau teaches JavaScript](https://www.youtube.com/watch?v=mVI-FD2f-wE)
