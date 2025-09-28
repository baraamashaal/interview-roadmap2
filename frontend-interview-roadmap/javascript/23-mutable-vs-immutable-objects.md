
# 23. Mutable vs. Immutable Objects in JavaScript

## Quick Revision

*   **Mutable:** An object is mutable if its state can be changed after it is created. In JavaScript, objects and arrays are mutable by default.

*   **Immutable:** An object is immutable if its state cannot be changed after it is created. To change an immutable object, you must create a new object with the updated values.

## Detailed Explanation

### Mutable Objects

Most objects in JavaScript are mutable. This means you can change their properties and values after they have been created.

```javascript
const person = { name: 'Baraa', age: 30 };
person.age = 31; // This is a mutation
console.log(person); // { name: 'Baraa', age: 31 }
```

While this is convenient, it can lead to unexpected side effects, especially in large applications. If you pass a mutable object to a function, that function can change the object, which may affect other parts of your application that are using the same object.

### Immutable Objects

Immutable objects cannot be changed after they are created. If you need to change an immutable object, you create a new object with the desired changes.

JavaScript does not have built-in immutable data structures, but you can achieve immutability through patterns and libraries.

#### Achieving Immutability

1.  **Manual approach (using `Object.assign` or spread syntax):**

    ```javascript
    const person = { name: 'Baraa', age: 30 };
    const updatedPerson = { ...person, age: 31 };
    ```

2.  **`Object.freeze()`:** This method freezes an object, preventing new properties from being added, existing properties from being removed, and existing properties from being changed. However, it only provides a shallow freeze.

    ```javascript
    const person = { name: 'Baraa', address: { city: 'Dubai' } };
    Object.freeze(person);

    person.age = 31; // This will not work
    person.address.city = 'Abu Dhabi'; // This WILL work because Object.freeze() is shallow
    ```

3.  **Libraries like Immer and Immutable.js:** These libraries provide efficient and easy-to-use immutable data structures.

    *   **Immer:** Uses a "copy-on-write" mechanism that makes it feel like you are mutating data, but it actually creates a new immutable object under the hood.
    *   **Immutable.js:** Provides a set of immutable data structures (e.g., `Map`, `List`).

## Benefits of Immutability

*   **Predictability:** Immutable objects are easier to reason about because their state never changes.
*   **Performance Optimization:** Immutability makes it easy to detect changes. If an object is immutable, you can simply check if the reference has changed to see if the object has been updated. This is used by libraries like React to optimize rendering.
*   **Concurrency:** Immutability simplifies concurrent programming because you don't have to worry about race conditions or other issues related to shared mutable state.

## Resources

*   **Article:** [MDN - Object.freeze()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)
*   **Article:** [The State of Immutability in JavaScript](https://www.freecodecamp.org/news/the-state-of-immutability-in-javascript-420291387e05/)
*   **Library:** [Immer](https://immerjs.github.io/immer/)
*   **Library:** [Immutable.js](https://immutable-js.github.io/immutable-js/)
