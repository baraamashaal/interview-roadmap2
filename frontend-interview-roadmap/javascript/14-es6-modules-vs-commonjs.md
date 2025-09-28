
# 14. ES6 Modules vs. CommonJS

## Quick Revision

**ES6 Modules** and **CommonJS** are two different module systems used in JavaScript to organize and reuse code.

*   **CommonJS (CJS):** The module system used in Node.js. It is synchronous and uses `require()` to import modules and `module.exports` to export them.

*   **ES6 Modules (ESM):** The standard module system for JavaScript, introduced in ES6. It is asynchronous and uses `import` and `export` statements.

## Detailed Explanation

### CommonJS (CJS)

*   **Syntax:**
    *   Import: `const myModule = require('./myModule');`
    *   Export: `module.exports = { ... };` or `exports.myFunction = ...;`
*   **Loading:** Synchronous. When you `require` a module, the execution of the current module is blocked until the required module is loaded and executed.
*   **Environment:** Primarily used in server-side JavaScript with Node.js.
*   **Bindings:** When you import a CommonJS module, you are importing a copy of the exported object. The bindings are not live.

### ES6 Modules (ESM)

*   **Syntax:**
    *   Import: `import myModule from './myModule';` or `import { myFunction } from './myModule';`
    *   Export: `export default { ... };` or `export const myFunction = ...;`
*   **Loading:** Asynchronous. ES modules are loaded and parsed in a way that allows for static analysis and optimizations like tree-shaking.
*   **Environment:** The standard for modern browsers and is also supported in Node.js (using `.mjs` files or by setting `"type": "module"` in `package.json`).
*   **Bindings:** ES modules export live bindings, not values. This means that if the value of an exported variable changes in the original module, the change will be reflected in the imported module.

### Key Differences

| Feature      | CommonJS                               | ES6 Modules                            |
|--------------|----------------------------------------|----------------------------------------|
| **Syntax**   | `require`, `module.exports`            | `import`, `export`                     |
| **Loading**  | Synchronous                            | Asynchronous                           |
| **Bindings** | Exports a copy of the value            | Exports a live binding                 |
| **Environment**| Primarily Node.js                      | Browsers and Node.js                   |
| **Static Analysis** | Not possible                           | Possible (enables tree-shaking)        |

## Code Examples

### CommonJS Example

```javascript
// myModule.js
const myFunction = () => {
  console.log('Hello from CommonJS!');
};
module.exports = { myFunction };

// main.js
const { myFunction } = require('./myModule');
myFunction();
```

### ES6 Modules Example

```javascript
// myModule.js
export const myFunction = () => {
  console.log('Hello from ES6 Modules!');
};

// main.js
import { myFunction } from './myModule.js';
myFunction();
```

## Which One to Use?

*   For modern frontend development (e.g., with React, Vue, Angular), always use **ES6 Modules**.
*   For Node.js development, you can use either, but ES6 Modules are becoming the standard.

## Resources

*   **Article:** [MDN - JavaScript modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)
*   **Article:** [Node.js Documentation - Modules](https://nodejs.org/api/modules.html)
*   **Article:** [CommonJS vs. ES Modules in Node.js](https://www.freecodecamp.org/news/commonjs-vs-es-modules-in-nodejs/)
