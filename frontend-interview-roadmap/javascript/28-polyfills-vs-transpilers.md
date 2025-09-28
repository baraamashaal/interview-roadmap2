
# 28. Polyfills vs. Transpilers in JavaScript

## Quick Revision

**Polyfills** and **transpilers** are both tools that help you use modern JavaScript features in older browsers that don't support them.

*   **Polyfill:** A piece of code (a polyfill) that provides the implementation of a modern feature that is missing in an older browser. It fills in the gaps in the browser's native API.

*   **Transpiler:** A tool that converts modern JavaScript code into an older version of JavaScript that is compatible with a wider range of browsers. The most common transpiler is **Babel**.

## Detailed Explanation

### Polyfills

A polyfill is a script that provides a modern API that is not available in an older browser. It essentially replicates the functionality of the new feature.

For example, if you want to use `Array.prototype.find()`, which was introduced in ES6, in an older browser that doesn't support it, you can include a polyfill for it.

**When to use polyfills:**

*   When a new feature can be implemented using existing JavaScript syntax.
*   For new methods on existing objects (e.g., `Array.prototype.find`, `Object.assign`).

### Transpilers

A transpiler (a portmanteau of "transformer" and "compiler") is a tool that reads source code written in one programming language and produces the equivalent code in another language.

In the context of JavaScript, a transpiler like **Babel** converts modern JavaScript code (e.g., ES6, ES7) into an older version of JavaScript (e.g., ES5) that is more widely supported by browsers.

**When to use transpilers:**

*   When a new feature is a new syntax that cannot be implemented with existing JavaScript (e.g., arrow functions, classes, `async/await`).

## Code Examples

### Polyfill Example (`Array.prototype.find`)

```javascript
// Polyfill for Array.prototype.find
if (!Array.prototype.find) {
  Object.defineProperty(Array.prototype, 'find', {
    value: function(predicate) {
      if (this == null) {
        throw new TypeError('"this" is null or not defined');
      }
      var o = Object(this);
      var len = o.length >>> 0;
      if (typeof predicate !== 'function') {
        throw new TypeError('predicate must be a function');
      }
      var thisArg = arguments[1];
      var k = 0;
      while (k < len) {
        var kValue = o[k];
        if (predicate.call(thisArg, kValue, k, o)) {
          return kValue;
        }
        k++;
      }
      return undefined;
    }
  });
}
```

### Transpiler Example (Babel)

**Modern JavaScript (ES6):**

```javascript
const add = (a, b) => a + b;
```

**Transpiled JavaScript (ES5):**

```javascript
"use strict";

var add = function add(a, b) {
  return a + b;
};
```

## How They Work Together

Polyfills and transpilers are often used together. A transpiler like Babel can be configured to automatically include polyfills for the features you are using.

For example, when Babel transpiles your code, it can identify that you are using `Object.assign` and automatically include a polyfill for it if the target browser doesn't support it.

## Resources

*   **Article:** [What is a Polyfill?](https://www.freecodecamp.org/news/what-is-a-polyfill/)
*   **Article:** [Babel Documentation](https://babeljs.io/docs/en/)
*   **Tool:** [Babel REPL](https://babeljs.io/repl)
