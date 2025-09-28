
# 22. Functional Programming in JavaScript

## Quick Revision

**Functional Programming (FP)** is a programming paradigm that treats computation as the evaluation of mathematical functions and avoids changing-state and mutable data. Key concepts in functional programming include:

*   **Pure Functions:** Functions that always produce the same output for the same input and have no side effects.
*   **Immutability:** Data should not be changed after it is created.
*   **First-Class Functions:** Functions are treated like any other variable; they can be passed as arguments to other functions, returned from functions, and assigned to variables.
*   **Higher-Order Functions:** Functions that take other functions as arguments or return them as results.

## Detailed Explanation

### Pure Functions

A pure function has two main characteristics:

1.  **Deterministic:** Given the same input, it will always return the same output.
2.  **No Side Effects:** It does not modify any state outside of its own scope (e.g., modifying a global variable, writing to a file, logging to the console).

```javascript
// Pure function
function add(a, b) {
  return a + b;
}

// Impure function
let total = 0;
function addToTotal(n) {
  total += n; // Side effect: modifies a global variable
  return total;
}
```

### Immutability

In functional programming, you should avoid modifying data directly. Instead, you should create new data structures with the updated values.

```javascript
// Mutable
const person = { name: 'Baraa', age: 30 };
person.age = 31; // Mutating the object

// Immutable
const person2 = { name: 'Mashaal', age: 30 };
const updatedPerson = { ...person2, age: 31 }; // Creating a new object
```

### First-Class and Higher-Order Functions

In JavaScript, functions are first-class citizens. This means they can be treated like any other value. This enables the use of higher-order functions, which are a cornerstone of functional programming.

`map`, `filter`, and `reduce` are classic examples of higher-order functions in JavaScript.

```javascript
const numbers = [1, 2, 3, 4, 5];

// map: creates a new array by applying a function to each element
const doubled = numbers.map(n => n * 2);

// filter: creates a new array with all elements that pass a test
const evens = numbers.filter(n => n % 2 === 0);

// reduce: applies a function against an accumulator and each element to reduce the array to a single value
const sum = numbers.reduce((acc, current) => acc + current, 0);
```

### Function Composition

Function composition is the process of combining two or more functions to produce a new function. The output of one function becomes the input of the next.

```javascript
const compose = (f, g) => (x) => f(g(x));

const toUpperCase = (str) => str.toUpperCase();
const exclaim = (str) => `${str}!`;

const shout = compose(exclaim, toUpperCase);

console.log(shout('hello')); // HELLO!
```

## Benefits of Functional Programming

*   **Predictability:** Pure functions are easier to reason about and test because they are deterministic.
*   **Readability:** Code can be more declarative and easier to understand.
*   **Concurrency:** Immutability makes it easier to write concurrent and parallel programs.

## Resources

*   **Article:** [An Introduction to Functional Programming in JavaScript](https://www.freecodecamp.org/news/an-introduction-to-functional-programming-in-javascript-e589e275749e/)
*   **Article:** [MDN - Functional programming](https://developer.mozilla.org/en-US/docs/Glossary/Functional_programming)
*   **Video:** [Functional Programming in JavaScript - Beau teaches JavaScript](https://www.youtube.com/watch?v=e-5obm1G_FY)
*   **Book:** [Composing Software by Eric Elliott](https://leanpub.com/composingsoftware)
