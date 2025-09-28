
# 9. Shallow vs. Deep Copy in JavaScript

## Quick Revision

*   **Shallow Copy:** A shallow copy of an object is a copy whose properties share the same references as those of the source object. If a property is a primitive type (e.g., string, number), the value is copied. If a property is a reference type (e.g., object, array), the reference is copied, not the actual object.

*   **Deep Copy:** A deep copy of an object is a copy whose properties do not share the same references as those of the source object. It recursively copies all properties, so you get a completely independent object.

## Detailed Explanation

### Shallow Copy

When you create a shallow copy, you are creating a new object, but the nested objects are not new. They are references to the original nested objects.

**Methods for creating a shallow copy:**

*   **`Object.assign()`**
*   **Spread syntax (`...`)**
*   **`Array.prototype.slice()`**
*   **`Array.prototype.concat()`**

Changes to nested objects in the copied object will affect the original object, and vice versa.

### Deep Copy

A deep copy creates a completely new object, including all nested objects. Changes to the copied object will not affect the original object.

**Methods for creating a deep copy:**

*   **`JSON.parse(JSON.stringify(object))`:** This is a simple way to create a deep copy, but it has some limitations:
    *   It does not work with functions, `undefined`, or symbols.
    *   It can have issues with certain data types like `Date` objects (they will be converted to strings).
*   **Libraries like Lodash (`_.cloneDeep()`)**: These libraries provide robust and reliable methods for creating deep copies.
*   **Custom recursive function:** You can write your own function to perform a deep copy.

## Code Examples

### Shallow Copy Example

```javascript
const original = {
  name: 'Baraa',
  address: {
    city: 'Dubai'
  }
};

const shallowCopy = { ...original };

// Modify the shallow copy
shallowCopy.name = 'Mashaal';
shallowCopy.address.city = 'Abu Dhabi';

console.log(original.name);       // Baraa (primitive type, not affected)
console.log(original.address.city); // Abu Dhabi (nested object, affected)
```

### Deep Copy Example (using `JSON.stringify`)

```javascript
const original = {
  name: 'Baraa',
  address: {
    city: 'Dubai'
  }
};

const deepCopy = JSON.parse(JSON.stringify(original));

// Modify the deep copy
deepCopy.name = 'Mashaal';
deepCopy.address.city = 'Abu Dhabi';

console.log(original.name);       // Baraa (not affected)
console.log(original.address.city); // Dubai (not affected)
```

### Deep Copy Example (using Lodash)

```javascript
const _ = require('lodash');

const original = {
  name: 'Baraa',
  address: {
    city: 'Dubai'
  }
};

const deepCopy = _.cloneDeep(original);

// Modify the deep copy
deepCopy.name = 'Mashaal';
deepCopy.address.city = 'Abu Dhabi';

console.log(original.name);       // Baraa (not affected)
console.log(original.address.city); // Dubai (not affected)
```

## Resources

*   **Article:** [MDN - Object.assign()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
*   **Article:** [freeCodeCamp: How to Clone an Object in JavaScript (Shallow and Deep Copy)](https://www.freecodecamp.org/news/how-to-clone-an-object-in-javascript-shallow-and-deep-copy/)
*   **Video:** [Shallow vs Deep Copy - Beau teaches JavaScript](https://www.youtube.com/watch?v=E35k-p-9-lI)
*   **Library:** [Lodash `_.cloneDeep()`](https://lodash.com/docs/4.17.15#cloneDeep)
