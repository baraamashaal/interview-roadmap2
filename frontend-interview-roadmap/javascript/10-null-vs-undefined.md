
# 10. Null vs. Undefined in JavaScript

## Quick Revision

*   **`undefined`**: A variable that has been declared but has not yet been assigned a value is `undefined`. It is the default value of uninitialized variables.

*   **`null`**: `null` is an assignment value. It can be assigned to a variable as a representation of no value. It is an intentional absence of any object value.

## Detailed Explanation

### `undefined`

`undefined` usually means that a variable has been declared, but it has not been assigned a value. It is a primitive type in JavaScript.

**Situations where `undefined` is returned:**

*   An uninitialized variable.
*   A function that does not explicitly return a value.
*   Accessing a non-existent property of an object.
*   A function parameter that is not passed a value.

### `null`

`null` is also a primitive type in JavaScript, but it represents the intentional absence of any object value. It is a value that you, as a developer, can assign to a variable.

### Key Differences

| Feature      | `undefined`                               | `null`                                      |
|--------------|-------------------------------------------|---------------------------------------------|
| **Type**     | `undefined`                               | `object` (this is a historical bug)         |
| **Meaning**  | A variable has been declared but not assigned a value. | A variable has been explicitly assigned a value of `null`. |
| **Use**      | The default value of uninitialized variables. | To represent the intentional absence of a value. |

### The `typeof` Bug

When you use the `typeof` operator on `null`, it returns `"object"`. This is a long-standing bug in JavaScript that cannot be fixed because it would break existing code.

```javascript
console.log(typeof undefined); // "undefined"
console.log(typeof null);      // "object"
```

### Comparison

When comparing `null` and `undefined`:

*   `null == undefined` is `true` (loose equality).
*   `null === undefined` is `false` (strict equality).

## Code Examples

### `undefined` Example

```javascript
let x;
console.log(x); // undefined

function doNothing() {}
console.log(doNothing()); // undefined

const obj = {};
console.log(obj.nonExistentProperty); // undefined
```

### `null` Example

```javascript
let y = null;
console.log(y); // null

function findUser(id) {
  if (id === 1) {
    return { name: 'Baraa' };
  } else {
    return null; // Intentionally return null if user is not found
  }
}

console.log(findUser(1)); // { name: 'Baraa' }
console.log(findUser(2)); // null
```

## Resources

*   **Article:** [MDN - undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)
*   **Article:** [MDN - null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null)
*   **Article:** [freeCodeCamp: The Nullish Coalescing Operator in JavaScript](https://www.freecodecamp.org/news/the-nullish-coalescing-operator-in-javascript/)
*   **Video:** [JavaScript Null vs Undefined - Beau teaches JavaScript](https://www.youtube.com/watch?v=10V_4XpL-cM)
