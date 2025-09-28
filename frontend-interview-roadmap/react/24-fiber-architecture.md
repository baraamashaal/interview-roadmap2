
# 24. React Fiber Architecture

## Quick Revision

**React Fiber** is a complete re-implementation of React's core reconciliation algorithm. It was introduced in React 16 to enable new features like incremental rendering, error boundaries, and Suspense. The main goal of Fiber is to make rendering interruptible and resumable, allowing React to prioritize updates and prevent the UI from freezing.

## Detailed Explanation

Before Fiber, React's reconciliation algorithm (Stack Reconciler) was a synchronous, recursive process. Once React started rendering, it wouldn't stop until the entire component tree was processed. This could lead to a poor user experience, especially for large and complex applications, as long-running rendering tasks would block the main thread and make the UI unresponsive.

### Key Concepts of Fiber

1.  **Incremental Rendering:** Fiber allows React to split the rendering work into smaller units and spread it out over multiple frames. This means React can pause rendering, let the browser handle more urgent tasks (like user input), and then resume rendering later.

2.  **Prioritization:** Fiber introduces a priority system for updates. High-priority updates (e.g., user input) can interrupt lower-priority updates (e.g., data fetching) to ensure a smooth user experience.

3.  **Work in Progress Tree:** Fiber works by building a "work in progress" tree (a Fiber tree) in memory. This tree is a representation of the component tree that is currently being rendered. Once the work is complete, the work in progress tree is swapped with the current tree, and the changes are committed to the DOM.

4.  **Two Phases of Rendering:** Fiber divides the rendering process into two main phases:

    *   **Render/Reconciliation Phase (Interruptible):** In this phase, React builds the Fiber tree, performs diffing, and calculates the changes that need to be made to the DOM. This phase can be paused and resumed.
    *   **Commit Phase (Uninterruptible):** In this phase, React applies the changes to the real DOM. This phase is synchronous and cannot be interrupted.

### Fiber Node

Each component in the React tree corresponds to a **Fiber node**. A Fiber node is a JavaScript object that contains information about a component, such as its type, props, state, and a pointer to its parent, child, and sibling Fiber nodes.

## Benefits of Fiber

*   **Improved Responsiveness:** By making rendering interruptible, Fiber ensures that the UI remains responsive even during complex updates.
*   **New Features:** Fiber enabled the implementation of new features like Suspense, Error Boundaries, and Concurrent Mode.
*   **Better User Experience:** A smoother and more fluid user experience.

## Resources

*   **Article:** [React Docs - React Fiber Architecture](https://reactjs.org/docs/design-principles/priorities.html)
*   **Article:** [A Cartoon Intro to Fiber](https://medium.com/@acdlite/a-cartoon-intro-to-fiber-b4993673a775)
*   **Video:** [A Cartoon Intro to Fiber - React Conf 2017](https://www.youtube.com/watch?v=ZCuYPiUIONs)
