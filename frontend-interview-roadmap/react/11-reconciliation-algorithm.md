
# 11. The Reconciliation Algorithm in React

## Quick Revision

**Reconciliation** is the process by which React updates the DOM to match the current state of the application. It is the algorithm that React uses to diff one tree with another to determine which parts need to be changed.

The key to React's efficient reconciliation algorithm is the **Virtual DOM**. When the state of a component changes, React creates a new virtual DOM tree and compares it with the previous one. This process is called **diffing**.

## Detailed Explanation

React's reconciliation algorithm is based on a set of heuristics that make the diffing process very fast. The two main heuristics are:

1.  **Different element types:** If the root elements of the two trees have different types, React will tear down the old tree and build a new one from scratch.

2.  **Lists of elements:** When rendering a list of elements, React uses **keys** to identify which elements have changed, been added, or been removed.

### The Diffing Algorithm

When diffing two trees, React first compares the two root elements.

#### 1. Elements of Different Types

If the root elements have different types, React will destroy the old tree and build a new one. For example, if you change an `<article>` to a `<section>`, React will destroy the old `<article>` and all of its children and create a new `<section>`.

#### 2. Elements of the Same Type

If the root elements have the same type, React will keep the same underlying DOM node and only update the changed attributes.

After updating the attributes, React will then recurse on the children of the two elements.

#### 3. Lists of Elements and Keys

When rendering a list of elements, React needs a way to identify which elements have changed. This is where **keys** come in.

Keys should be **stable, predictable, and unique**. They help React identify which items have changed, been added, or been removed.

Without keys, React would have to rely on the order of the elements, which can be inefficient and lead to bugs.

## Fiber Architecture

In React 16, the reconciliation algorithm was rewritten and named **Fiber**. The Fiber architecture allows React to:

*   **Split rendering work into chunks:** This prevents long-running rendering tasks from blocking the main thread.
*   **Prioritize different types of work:** For example, user input can be prioritized over other updates.
*   **Pause, abort, or reuse work:** This makes rendering more efficient.

## Resources

*   **Article:** [React Docs - Reconciliation](https://reactjs.org/docs/reconciliation.html)
*   **Article:** [The `key` Prop in React](https://kentcdodds.com/blog/the-key-prop-in-react)
*   **Video:** [A Cartoon Intro to Fiber - React Conf 2017](https://www.youtube.com/watch?v=ZCuYPiUIONs)
