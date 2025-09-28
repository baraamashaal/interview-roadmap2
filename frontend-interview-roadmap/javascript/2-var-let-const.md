
# 2. What is the difference between var, let, and const in JavaScript?

## Quick Revision

*   **`var`**: Function-scoped, can be redeclared and updated. Hoisted to the top of its function scope.
*   **`let`**: Block-scoped, can be updated but not redeclared within the same scope. Hoisted but not initialized (in the Temporal Dead Zone).
*   **`const`**: Block-scoped, cannot be updated or redeclared. Must be initialized at the time of declaration. Hoisted but not initialized (in the Temporal Dead Zone).

## Detailed Explanation

### `var`

Before ES6, `var` was the only way to declare variables in JavaScript.

*   **Scope**: `var` declarations are function-scoped. This means they are only available within the function they are declared in. If declared outside of any function, they are globally scoped.
*   **Hoisting**: `var` variables are hoisted to the top of their scope and initialized with `undefined`. This means you can access a `var` variable before it's declared, and its value will be `undefined`.
*   **Redeclaration and Reassignment**: `var` variables can be redeclared and reassigned within the same scope.

### `let`

ES6 introduced `let` to provide block-level scoping.

*   **Scope**: `let` declarations are block-scoped (`{}`). This means they are only available within the block they are declared in (e.g., inside an `if` statement or a `for` loop).
*   **Hoisting and the Temporal Dead Zone (TDZ)**: `let` variables are hoisted but not initialized. Accessing a `let` variable before its declaration results in a `ReferenceError`. The period from the start of the block until the declaration is called the Temporal Dead Zone.
*   **Redeclaration and Reassignment**: `let` variables can be reassigned but not redeclared in the same scope.

### `const`

`const` is also block-scoped and was introduced in ES6.

*   **Scope**: `const` declarations are block-scoped, just like `let`.
*   **Hoisting and the Temporal Dead Zone (TDZ)**: `const` variables are also hoisted but not initialized, and they are in the TDZ.
*   **Redeclaration and Reassignment**: `const` variables cannot be reassigned or redeclared. They must be initialized at the time of declaration.

**Important Note on `const` with Objects and Arrays:**

When you declare an object or an array with `const`, the variable itself cannot be reassigned to a new object or array. However, the properties of the object or the elements of the array can be modified.

## Code Examples

### Scope Example

```javascript
function scopeTest() {
  var varVar = 'I am a var';
  if (true) {
    let letVar = 'I am a let';
    const constVar = 'I am a const';
    console.log(varVar); // Accessible
    console.log(letVar); // Accessible
    console.log(constVar); // Accessible
  }
  console.log(varVar); // Accessible
  // console.log(letVar); // ReferenceError: letVar is not defined
  // console.log(constVar); // ReferenceError: constVar is not defined
}
scopeTest();
```

### Hoisting Example

```javascript
console.log(hoistedVar); // undefined
var hoistedVar = 'I am hoisted';

// console.log(hoistedLet); // ReferenceError: Cannot access 'hoistedLet' before initialization
// let hoistedLet = 'I am not initialized';
```

### `const` with Objects

```javascript
const person = {
  name: 'Baraa'
};

// This is allowed
person.name = 'Mashaal';
console.log(person.name); // Mashaal

// This is NOT allowed
// person = { name: 'John' }; // TypeError: Assignment to constant variable.
```

## Resources

*   **Article:** [MDN - let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
*   **Article:** [MDN - const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
*   **Article:** [freeCodeCamp: var, let, and const – What's the Difference?](https://www.freecodecamp.org/news/var-let-and-const-whats-the-difference/)
*   **Video:** [var, let and const - ES6 JavaScript Features](https://www.youtube.com/watch?v=s-7T000a-w0)
