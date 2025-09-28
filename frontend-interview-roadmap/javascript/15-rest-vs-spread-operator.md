
# 15. Rest vs. Spread Operator in JavaScript

## Quick Revision

The rest and spread operators use the same syntax (`...`), but they have opposite functions.

*   **Rest Operator (`...`):** Collects multiple elements and "condenses" them into a single array. It is used in function parameters to gather all remaining arguments into an array.

*   **Spread Operator (`...`):** "Expands" an iterable (like an array or string) into individual elements. It is used to spread the elements of an array or object into another array or object.

## Detailed Explanation

### Rest Operator

The rest operator is used to represent an indefinite number of arguments as an array.

*   It must be the last parameter in a function definition.
*   It gathers all remaining arguments into an array.

```javascript
function sum(...numbers) {
  return numbers.reduce((acc, current) => acc + current, 0);
}

console.log(sum(1, 2, 3)); // 6
console.log(sum(1, 2, 3, 4, 5)); // 15
```

### Spread Operator

The spread operator is used to expand an iterable into individual elements.

**Use Cases for Spread Operator:**

*   **Combining arrays:**

    ```javascript
    const arr1 = [1, 2, 3];
    const arr2 = [4, 5, 6];
    const combined = [...arr1, ...arr2]; // [1, 2, 3, 4, 5, 6]
    ```

*   **Copying an array (shallow copy):**

    ```javascript
    const original = [1, 2, 3];
    const copy = [...original];
    ```

*   **Passing arguments to a function:**

    ```javascript
    function multiply(a, b, c) {
      return a * b * c;
    }
    const nums = [2, 3, 4];
    console.log(multiply(...nums)); // 24
    ```

*   **Spreading properties of an object (ES2018):**

    ```javascript
    const obj1 = { a: 1, b: 2 };
    const obj2 = { c: 3, d: 4 };
    const combinedObj = { ...obj1, ...obj2 }; // { a: 1, b: 2, c: 3, d: 4 }
    ```

## Code Examples

### Rest Operator in Function Parameters

```javascript
function logArgs(firstArg, ...restOfArgs) {
  console.log('First argument:', firstArg);
  console.log('Rest of arguments:', restOfArgs);
}

logArgs('a', 'b', 'c', 'd');
// First argument: a
// Rest of arguments: [ 'b', 'c', 'd' ]
```

### Spread Operator for Cloning and Merging

```javascript
const person = { name: 'Baraa', age: 30 };
const address = { city: 'Dubai', country: 'UAE' };

const personWithAddress = { ...person, ...address };
console.log(personWithAddress);
// { name: 'Baraa', age: 30, city: 'Dubai', country: 'UAE' }

const numbers = [1, 2, 3];
const newNumbers = [...numbers, 4, 5];
console.log(newNumbers); // [ 1, 2, 3, 4, 5 ]
```

## Resources

*   **Article:** [MDN - Rest parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)
*   **Article:** [MDN - Spread syntax (...)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
*   **Article:** [JavaScript Rest vs Spread Operator](https://www.freecodecamp.org/news/javascript-rest-vs-spread-operator/)
*   **Video:** [JavaScript Rest and Spread - Beau teaches JavaScript](https://www.youtube.com/watch?v=iLx4ma8ZqvQ)
