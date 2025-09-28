
# 13. How Does `this` Work in Different Contexts in JavaScript?

## Quick Revision

The value of the `this` keyword in JavaScript depends on the context in which it is used. It is a reference to the object that is currently executing the function.

*   **Global Context:** In the global scope, `this` refers to the global object (`window` in browsers).
*   **Function Context:** In a simple function call, `this` is the global object (or `undefined` in strict mode).
*   **Method Context:** When a function is called as a method of an object, `this` refers to the object that the method is called on.
*   **Constructor Context:** When a function is used as a constructor (with the `new` keyword), `this` refers to the newly created object.
*   **Arrow Functions:** Arrow functions do not have their own `this` binding. They inherit `this` from the enclosing lexical scope.
*   **Explicit Binding:** You can explicitly set the value of `this` using `call()`, `apply()`, and `bind()`.

## Detailed Explanation

### 1. Global Context

In the global execution context (outside of any function), `this` refers to the global object.

```javascript
console.log(this); // window (in a browser)
```

### 2. Function Context

In a regular function call, the value of `this` depends on whether the code is in strict mode.

*   **Non-strict mode:** `this` is the global object.
*   **Strict mode:** `this` is `undefined`.

```javascript
function showThis() {
  console.log(this);
}

showThis(); // window (in non-strict mode)

function showThisStrict() {
  'use strict';
  console.log(this);
}

showThisStrict(); // undefined
```

### 3. Method Context

When a function is called as a method of an object, `this` refers to the object that the method is a part of.

```javascript
const person = {
  name: 'Baraa',
  greet: function() {
    console.log(`Hello, ${this.name}`);
  }
};

person.greet(); // Hello, Baraa
```

### 4. Constructor Context

When a function is used as a constructor with the `new` keyword, `this` is bound to the new object being created.

```javascript
function Person(name) {
  this.name = name;
}

const baraa = new Person('Baraa');
console.log(baraa.name); // Baraa
```

### 5. Arrow Functions

Arrow functions do not have their own `this` context. Instead, they capture the `this` value of the enclosing lexical context.

```javascript
const person = {
  name: 'Baraa',
  hobbies: ['reading', 'coding'],
  printHobbies: function() {
    this.hobbies.forEach(hobby => {
      // 'this' is inherited from the printHobbies method
      console.log(`${this.name} likes ${hobby}`);
    });
  }
};

person.printHobbies();
```

### 6. Explicit Binding with `call()`, `apply()`, and `bind()`

*   **`call(thisArg, arg1, arg2, ...)`:** Calls a function with a given `this` value and arguments provided individually.
*   **`apply(thisArg, [argsArray])`:** Calls a function with a given `this` value and an array of arguments.
*   **`bind(thisArg)`:** Creates a new function that, when called, has its `this` keyword set to the provided value.

```javascript
function greet() {
  console.log(`Hello, ${this.name}`);
}

const person1 = { name: 'Baraa' };
const person2 = { name: 'Mashaal' };

greet.call(person1);  // Hello, Baraa
greet.apply(person2); // Hello, Mashaal

const greetBaraa = greet.bind(person1);
greetBaraa(); // Hello, Baraa
```

## Resources

*   **Article:** [MDN - this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
*   **Article:** [A Deep Dive into `this` in JavaScript](https://www.freecodecamp.org/news/a-deep-dive-into-this-in-javascript-491414339554/)
*   **Video:** [JavaScript 'this' Keyword - Beau teaches JavaScript](https://www.youtube.com/watch?v=gvicrj31JOM)
