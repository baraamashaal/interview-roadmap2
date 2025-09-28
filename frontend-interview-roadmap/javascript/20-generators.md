
# 20. Generators in JavaScript

## Quick Revision

**Generator functions** are a special type of function in JavaScript that can be paused and resumed. They are defined using the `function*` syntax and use the `yield` keyword to pause execution and return a value.

When a generator function is called, it does not execute the function body immediately. Instead, it returns a **generator object**, which is an iterator. You can then call the `next()` method on the generator object to execute the function until the next `yield` statement.

## Detailed Explanation

Generator functions allow you to define an iterative algorithm by writing a single function whose execution is not continuous.

### Key Concepts

*   **`function*`:** The syntax for defining a generator function.
*   **`yield`:** The `yield` keyword pauses the generator's execution and returns the value of the expression following the `yield` keyword.
*   **Generator Object:** The object returned by a generator function. It conforms to both the iterable and iterator protocols.
*   **`next()` method:** When you call `next()`, the generator function executes until it encounters a `yield` statement. The `next()` method returns an object with two properties:
    *   `value`: The value yielded by the `yield` statement.
    *   `done`: A boolean value that is `true` if the generator has finished, and `false` otherwise.

### Two-Way Communication

Generators also allow for two-way communication. You can pass a value to the `next()` method, and that value will be the result of the `yield` expression.

## Code Examples

### Basic Generator Example

```javascript
function* myGenerator() {
  yield 1;
  yield 2;
  yield 3;
}

const gen = myGenerator();

console.log(gen.next()); // { value: 1, done: false }
console.log(gen.next()); // { value: 2, done: false }
console.log(gen.next()); // { value: 3, done: false }
console.log(gen.next()); // { value: undefined, done: true }
```

### Using a Generator for an Infinite Sequence

```javascript
function* idGenerator() {
  let id = 1;
  while (true) {
    yield id++;
  }
}

const idGen = idGenerator();

console.log(idGen.next().value); // 1
console.log(idGen.next().value); // 2
console.log(idGen.next().value); // 3
```

### Two-Way Communication Example

```javascript
function* twoWayGenerator() {
  const name = yield 'What is your name?';
  console.log(`Hello, ${name}!`);
}

const twoWayGen = twoWayGenerator();

console.log(twoWayGen.next().value); // What is your name?
console.log(twoWayGen.next('Baraa')); // Hello, Baraa!
```

## Use Cases

*   **Iterators:** Generators provide a simple way to create custom iterators.
*   **Asynchronous Programming:** Generators were used to manage asynchronous code before `async/await` became the standard. Libraries like `co.js` used generators to write asynchronous code that looked synchronous. `async/await` is essentially syntactic sugar over generators.
*   **State Machines:** Generators can be used to implement state machines.

## Resources

*   **Article:** [MDN - function*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*)
*   **Article:** [JavaScript Generators for Beginners](https://www.freecodecamp.org/news/javascript-generators-for-beginners/)
*   **Video:** [JavaScript Generators - Beau teaches JavaScript](https://www.youtube.com/watch?v=W4p_2c5f_cU)
