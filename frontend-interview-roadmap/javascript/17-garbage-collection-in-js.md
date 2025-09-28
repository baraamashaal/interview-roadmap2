
# 17. Garbage Collection in JavaScript

## Quick Revision

**Garbage Collection (GC)** is the process of automatically freeing up memory that is no longer in use by an application. In JavaScript, the garbage collector runs periodically to identify and reclaim memory from objects that are no longer reachable.

The most common algorithm used by modern garbage collectors is the **mark-and-sweep** algorithm.

## Detailed Explanation

JavaScript provides automatic memory management, which means that developers don't have to manually allocate and deallocate memory. This is handled by the JavaScript engine's garbage collector.

### The Memory Lifecycle

1.  **Allocate memory:** When you create a variable, function, or object, the JavaScript engine allocates memory for it.
2.  **Use memory:** You read and write to the allocated memory.
3.  **Release memory:** When the memory is no longer needed, the garbage collector frees it up.

### The Mark-and-Sweep Algorithm

The mark-and-sweep algorithm is the most common garbage collection algorithm.

1.  **Root:** The algorithm starts from a set of "roots". In JavaScript, the global object is a root.
2.  **Mark:** The garbage collector traverses the object graph starting from the roots and "marks" every object it can reach.
3.  **Sweep:** The garbage collector then scans the heap and "sweeps" away all the unmarked objects, freeing up their memory.

An object is considered "garbage" if it is no longer reachable from any root.

### Reachability

An object is considered **reachable** if it is accessible from a root, either directly or indirectly through a chain of references.

*   A set of base values that are inherently reachable (e.g., global variables, the current function's local variables).
*   Any value that is referenced by a reachable value is also considered reachable.

### Example

```javascript
let person = {
  name: 'Baraa',
  address: {
    city: 'Dubai'
  }
};

// The 'person' object and its 'address' object are reachable.

let address = person.address;

person = null; // The 'person' object is no longer directly reachable from the root.
// However, the 'address' object is still reachable through the 'address' variable.

address = null; // Now the 'address' object is no longer reachable and can be garbage collected.
// Since the 'person' object is also no longer reachable, it can also be garbage collected.
```

### Memory Leaks

Memory leaks occur when memory is no longer needed but is not released because it is still reachable. (See question 11 for more details on memory leaks).

## Resources

*   **Article:** [MDN - Memory Management](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management)
*   **Article:** [Visualizing Garbage Collection in V8](https://dev.to/deepu105/visualizing-garbage-collection-in-v8-4f02)
*   **Video:** [Garbage Collection - Beau teaches JavaScript](https://www.youtube.com/watch?v=h_J_Vq-L-gE)
