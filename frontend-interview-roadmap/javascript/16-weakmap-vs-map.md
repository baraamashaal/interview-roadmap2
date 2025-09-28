
# 16. WeakMap vs. Map in JavaScript

## Quick Revision

**`Map`** and **`WeakMap`** are both key-value collections in JavaScript.

*   **`Map`**: Can have keys of any type (including objects). It keeps a strong reference to its keys, which means that as long as the `Map` exists, the keys will not be garbage collected.

*   **`WeakMap`**: Can only have objects as keys. It keeps a weak reference to its keys, which means that if an object key is the only reference to that object, it can be garbage collected. This makes `WeakMap` useful for memory management.

## Detailed Explanation

### `Map`

The `Map` object holds key-value pairs and remembers the original insertion order of the keys.

*   **Keys:** Any value (both objects and primitive values) may be used as a key.
*   **References:** `Map` keeps strong references to its keys. This means that if you have an object as a key in a `Map`, that object will not be garbage collected as long as the `Map` exists.
*   **Iteration:** `Map` is iterable. You can use `forEach`, `for...of`, and other iteration methods.

### `WeakMap`

The `WeakMap` object is a collection of key/value pairs in which the keys are weakly referenced.

*   **Keys:** The keys of a `WeakMap` must be objects. Primitive data types are not allowed.
*   **References:** `WeakMap` holds its keys "weakly". This means that if an object that is used as a key in a `WeakMap` has no other references, it can be garbage collected. When the key is garbage collected, the corresponding value is also removed from the `WeakMap`.
*   **Iteration:** `WeakMap` is not iterable. This is because the list of keys can change at any time due to garbage collection.

### Key Differences

| Feature      | `Map`                                  | `WeakMap`                              |
|--------------|----------------------------------------|----------------------------------------|
| **Keys**     | Any type                               | Objects only                           |
| **References**| Strong                                 | Weak                                   |
| **Iteration**| Iterable                               | Not iterable                           |
| **Use Case** | General-purpose key-value storage      | Storing metadata about objects without preventing garbage collection |

## Code Examples

### `Map` Example

```javascript
let myMap = new Map();
let myObj = { name: 'Baraa' };

myMap.set(myObj, 'some metadata');

console.log(myMap.has(myObj)); // true

myObj = null; // The object is still in memory because the Map has a strong reference to it

console.log(myMap.keys().next().value); // { name: 'Baraa' }
```

### `WeakMap` Example

```javascript
let myWeakMap = new WeakMap();
let myObj = { name: 'Mashaal' };

myWeakMap.set(myObj, 'some other metadata');

console.log(myWeakMap.has(myObj)); // true

myObj = null; // Now the object can be garbage collected

// There is no way to verify that the object has been removed from the WeakMap
// because WeakMaps are not iterable.
```

## When to Use `WeakMap`

`WeakMap` is useful when you want to associate some data with an object without preventing that object from being garbage collected. A common use case is to store metadata about an object that is only relevant as long as the object is in use.

For example, you could use a `WeakMap` to store a cache of computed values for an object. If the object is garbage collected, the cached values will be automatically removed from the `WeakMap`.

## Resources

*   **Article:** [MDN - Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)
*   **Article:** [MDN - WeakMap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap)
*   **Article:** [JavaScript `Map` vs `WeakMap`](https://www.freecodecamp.org/news/javascript-map-vs-weakmap/)
