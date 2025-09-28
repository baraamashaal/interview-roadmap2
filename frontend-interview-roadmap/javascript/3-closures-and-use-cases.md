
# 3. Explain Closures and Their Use Cases in JavaScript

## Quick Revision

A **closure** is a function that has access to its outer function's scope, even after the outer function has returned. In other words, a closure gives you access to an outer function's scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

## Detailed Explanation

A closure is the combination of a function and the lexical environment within which that function was declared. This environment consists of any local variables that were in-scope at the time the closure was created.

When a function is defined inside another function, the inner function has access to the variables of the outer function. This is called lexical scoping. The inner function "remembers" the environment in which it was created.

### How Closures Work

1.  When a function is executed, it creates a new execution context with its own set of local variables.
2.  If a function is defined inside another function, the inner function is lexically bound to the execution context of the outer function.
3.  When the outer function returns, its execution context is removed from the call stack. However, if the inner function is returned or otherwise made available outside the outer function, the variables of the outer function are still accessible to the inner function. This is the closure.

## Use Cases

### 1. Data Privacy (Encapsulation)

Closures can be used to create private variables and methods, a fundamental concept in object-oriented programming.

```javascript
function createCounter() {
  let count = 0; // This variable is private

  return {
    increment: function() {
      count++;
      return count;
    },
    decrement: function() {
      count--;
      return count;
    },
    getCount: function() {
      return count;
    }
  };
}

const counter = createCounter();
console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.getCount());   // 2
// console.log(counter.count); // undefined - cannot access the private variable
```

### 2. Function Factories

Closures can be used to create functions with a specific context.

```javascript
function createMultiplier(factor) {
  return function(number) {
    return number * factor;
  };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);

console.log(double(5)); // 10
console.log(triple(5)); // 15
```

### 3. Callbacks and Higher-Order Functions

Closures are essential for working with asynchronous code and callbacks.

```javascript
function fetchData(url, callback) {
  // Simulate an API call
  setTimeout(() => {
    const data = { message: 'Data fetched successfully!' };
    callback(data);
  }, 1000);
}

fetchData('https://api.example.com/data', (data) => {
  console.log(data.message); // Accesses the 'data' variable from the outer scope
});
```

### 4. Currying

Currying is a technique of evaluating a function with multiple arguments, into a sequence of functions with a single argument. Closures make currying possible in JavaScript.

```javascript
const curry = (fn) => {
  return function curried(...args) {
    if (args.length >= fn.length) {
      return fn.apply(this, args);
    } else {
      return function(...args2) {
        return curried.apply(this, args.concat(args2));
      }
    }
  };
};

const sum = (a, b, c) => a + b + c;
const curriedSum = curry(sum);

console.log(curriedSum(1)(2)(3)); // 6
console.log(curriedSum(1, 2)(3)); // 6
```

## Resources

*   **Article:** [MDN - Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
*   **Article:** [JavaScript Closures for Dummies](https://www.freecodecamp.org/news/javascript-closures-for-dummies/)
*   **Video:** [JavaScript Closures - W3Schools](https://www.youtube.com/watch?v=vKJ_b2r1A4s)
*   **Course:** [JavaScript: The Hard Parts, v2](https://frontendmasters.com/courses/javascript-hard-parts-v2/)
