
# 29. `for...in` vs. `for...of` in JavaScript

## Quick Revision

*   **`for...in`:** Iterates over the **enumerable properties** of an object. It is used for iterating over the keys of an object.

*   **`for...of`:** Iterates over the **values** of an iterable object (e.g., `Array`, `String`, `Map`, `Set`). It is used for iterating over the values in a collection.

## Detailed Explanation

### `for...in`

The `for...in` loop iterates over the enumerable properties of an object, including inherited properties from the prototype chain.

**Key characteristics:**

*   Iterates over property names (keys).
*   The order of iteration is not guaranteed.
*   It will iterate over inherited properties.

It is generally not recommended to use `for...in` to iterate over an array because it can have unexpected results.

### `for...of`

The `for...of` loop, introduced in ES6, iterates over the values of an iterable object.

**Key characteristics:**

*   Iterates over values.
*   The order of iteration is determined by the iterable's protocol.
*   It only iterates over the object's own properties, not inherited ones.

**Iterable objects include:**

*   `Array`
*   `String`
*   `Map`
*   `Set`
*   `arguments` object
*   DOM `NodeList`

Plain objects are not iterable by default.

## Code Examples

### `for...in` with an Object

```javascript
const person = { name: 'Baraa', age: 30 };

for (const key in person) {
  console.log(key); // name, age
  console.log(person[key]); // Baraa, 30
}
```

### `for...of` with an Array

```javascript
const numbers = [1, 2, 3];

for (const value of numbers) {
  console.log(value); // 1, 2, 3
}
```

### `for...in` vs. `for...of` with an Array

```javascript
const arr = ['a', 'b', 'c'];

console.log('for...in:');
for (const i in arr) {
  console.log(i); // 0, 1, 2 (the indices)
}

console.log('for...of:');
for (const v of arr) {
  console.log(v); // a, b, c (the values)
}
```

## When to Use Which

*   Use **`for...in`** when you need to iterate over the keys of an object.
*   Use **`for...of`** when you need to iterate over the values of an iterable object like an array or a string.

## Resources

*   **Article:** [MDN - for...in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)
*   **Article:** [MDN - for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)
*   **Article:** [`for...in` vs. `for...of` Loops in JavaScript](https://www.freecodecamp.org/news/for-in-vs-for-of-loops-in-javascript/)
