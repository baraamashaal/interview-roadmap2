
# 6. Explain Prototypal Inheritance in JavaScript

## Quick Revision

**Prototypal Inheritance** is a fundamental concept in JavaScript where objects can inherit properties and methods from other objects. Every JavaScript object has a private property called `[[Prototype]]` (exposed as `__proto__` or accessible via `Object.getPrototypeOf()`) that links to another object, called its **prototype**. When you try to access a property of an object, if the property is not found on the object itself, the JavaScript engine looks for the property on the object's prototype, and so on, up the **prototype chain**, until it finds the property or reaches the end of the chain (`null`).

## Detailed Explanation

Unlike class-based inheritance in languages like Java or C++, JavaScript uses a prototypal inheritance model. This means that objects inherit directly from other objects.

### The Prototype Chain

When you create an object in JavaScript, it is linked to a prototype object. This prototype object can also have its own prototype, and so on. This sequence of linked objects is called the **prototype chain**.

The chain ends when a prototype is `null`. `Object.prototype` is at the top of the prototype chain for most objects, and its prototype is `null`.

### How Property Access Works

When you access a property of an object:

1.  The JavaScript engine first checks if the property exists on the object itself.
2.  If it doesn't, it checks the object's prototype.
3.  If it's still not found, it continues up the prototype chain until it finds the property or reaches the end of the chain.
4.  If the property is not found anywhere in the chain, it returns `undefined`.

### Creating Objects and Inheritance

There are several ways to create objects and set up inheritance in JavaScript:

1.  **Constructor Functions:** Before ES6 classes, constructor functions were the primary way to create objects with a shared prototype.

2.  **`Object.create()`:** This method creates a new object with the specified prototype object and properties.

3.  **ES6 Classes:** ES6 introduced the `class` syntax, which is syntactic sugar over JavaScript's existing prototypal inheritance. It provides a more familiar syntax for developers coming from class-based languages.

## Code Examples

### Constructor Function Example

```javascript
// Parent constructor
function Animal(name) {
  this.name = name;
}

// Add a method to the Animal prototype
Animal.prototype.sayHello = function() {
  console.log(`Hello, I'm ${this.name}`);
};

// Child constructor
function Dog(name, breed) {
  // Call the parent constructor
  Animal.call(this, name);
  this.breed = breed;
}

// Set up the prototype chain
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog; // Reset the constructor property

// Add a method to the Dog prototype
Dog.prototype.bark = function() {
  console.log('Woof!');
};

const myDog = new Dog('Rex', 'German Shepherd');
myDog.sayHello(); // Hello, I'm Rex (inherited from Animal)
myDog.bark();     // Woof!
```

### `Object.create()` Example

```javascript
const animal = {
  sayHello: function() {
    console.log(`Hello, I'm ${this.name}`);
  }
};

const dog = Object.create(animal);
dog.name = 'Fido';
dog.bark = function() {
  console.log('Woof!');
};

dog.sayHello(); // Hello, I'm Fido
dog.bark();     // Woof!
```

### ES6 Class Example

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  sayHello() {
    console.log(`Hello, I'm ${this.name}`);
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name); // Call the parent constructor
    this.breed = breed;
  }

  bark() {
    console.log('Woof!');
  }
}

const myNewDog = new Dog('Buddy', 'Golden Retriever');
myNewDog.sayHello(); // Hello, I'm Buddy
myNewDog.bark();     // Woof!
```

## Resources

*   **Article:** [MDN - Inheritance and the prototype chain](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)
*   **Article:** [A Beginner's Guide to JavaScript's Prototype](https://www.freecodecamp.org/news/a-beginners-guide-to-javascripts-prototype-p2/)
*   **Video:** [Prototypal Inheritance - Beau teaches JavaScript](https://www.youtube.com/watch?v=iG_j8jsffM8)
*   **Course:** [JavaScript: The Hard Parts, v2](https://frontendmasters.com/courses/javascript-hard-parts-v2/)
