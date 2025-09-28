
# 4. Explain Hoisting in JavaScript

## Quick Revision

**Hoisting** is JavaScript's default behavior of moving declarations to the top of their scope before code execution. This means that `var` variable declarations and function declarations are processed before any code is executed. `let` and `const` are also hoisted, but they are not initialized, leading to a `ReferenceError` if accessed before declaration (Temporal Dead Zone).

## Detailed Explanation

Hoisting is a result of how JavaScript's execution context works. When a JavaScript engine executes a script, it creates an execution context in two phases:

1.  **Creation Phase:** The engine scans the code for variable and function declarations.
    *   **`var` variables:** Are declared and initialized with `undefined`.
    *   **`let` and `const` variables:** Are declared but **not** initialized. They are in a "Temporal Dead Zone" (TDZ).
    *   **Function declarations:** Are fully hoisted, meaning the function can be called before it is declared.
    *   **Function expressions:** Are not fully hoisted. If assigned to a `var`, the variable is hoisted and initialized with `undefined`. If assigned to `let` or `const`, the variable is hoisted but not initialized.

2.  **Execution Phase:** The engine executes the code line by line.

### Hoisting with `var`

`var` variables are hoisted to the top of their scope and initialized with `undefined`.

```javascript
console.log(myVar); // Outputs: undefined
var myVar = 10;
console.log(myVar); // Outputs: 10
```

### Hoisting with `let` and `const` (Temporal Dead Zone)

`let` and `const` are hoisted, but they are not initialized with a default value. Accessing them before the declaration results in a `ReferenceError`. The time between the start of the block and the variable declaration is the Temporal Dead Zone (TDZ).

```javascript
// console.log(myLet); // ReferenceError: Cannot access 'myLet' before initialization
let myLet = 20;
console.log(myLet); // Outputs: 20
```

### Hoisting with Function Declarations

Function declarations are fully hoisted, including the function body.

```javascript
hello(); // Outputs: "Hello, World!"

function hello() {
  console.log("Hello, World!");
}
```

### Hoisting with Function Expressions

Function expressions are not fully hoisted. The hoisting behavior depends on the variable declaration (`var`, `let`, or `const`).

```javascript
// console.log(sayGoodbye); // undefined (if declared with var)
// sayGoodbye(); // TypeError: sayGoodbye is not a function

var sayGoodbye = function() {
  console.log("Goodbye!");
};

sayGoodbye(); // Outputs: "Goodbye!"
```

## Code Examples

### `var` vs. `let` Hoisting

```javascript
function hoistingTest() {
  console.log('1. var a:', a); // undefined
  // console.log('2. let b:', b); // ReferenceError

  var a = 10;
  let b = 20;

  console.log('3. var a:', a); // 10
  console.log('4. let b:', b); // 20
}

hoistingTest();
```

### Function Declaration vs. Function Expression

```javascript
// Function Declaration - Hoisted
canBeCalledBeforeDeclaration(); // Works!

function canBeCalledBeforeDeclaration() {
  console.log('Function declaration was hoisted.');
}

// Function Expression - Not fully hoisted
// cannotBeCalledBeforeDeclaration(); // TypeError: cannotBeCalledBeforeDeclaration is not a function

var cannotBeCalledBeforeDeclaration = function() {
  console.log('Function expression was not fully hoisted.');
};
```

## Resources

*   **Article:** [MDN - Hoisting](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)
*   **Article:** [DigitalOcean: Hoisting in JavaScript](https://www.digitalocean.com/community/tutorials/hoisting-in-javascript)
*   **Video:** [JavaScript Hoisting - Beau teaches JavaScript](https://www.youtube.com/watch?v=C1PhtK-H3_M)
*   **Course:** [JavaScript: The Hard Parts, v2](https://frontendmasters.com/courses/javascript-hard-parts-v2/)
