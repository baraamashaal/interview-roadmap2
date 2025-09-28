
# 5. BEM Methodology

## Quick Revision

**BEM (Block, Element, Modifier)** is a naming convention for CSS classes that aims to make frontend development more organized, scalable, and maintainable. It helps developers write modular and reusable CSS by providing a strict structure for class names.

*   **Block:** A standalone, independent component (e.g., `header`, `menu`, `button`).
*   **Element:** A part of a block that has no standalone meaning (e.g., `menu__item`, `button__icon`).
*   **Modifier:** A flag on a block or an element that changes its appearance or behavior (e.g., `button--primary`, `menu__item--disabled`).

## Detailed Explanation

BEM helps solve common problems in CSS development, such as naming collisions, specificity issues, and difficulty in understanding the relationship between CSS rules and HTML structure.

### 1. Block

A Block is a functionally independent page component that can be reused. It can be simple or compound (contain other blocks).

**Naming:** Block names should be nouns or adjectives (e.g., `header`, `search-form`, `card`).

### 2. Element

An Element is a part of a block that performs a specific function and is semantically tied to its block. Elements cannot be used outside of their parent block.

**Naming:** Element names are separated from the block name by two underscores (`__`) (e.g., `block__element`).

### 3. Modifier

A Modifier is a flag on a block or an element. It is used to change the appearance, state, or behavior of a block or an element.

**Naming:** Modifier names are separated from the block or element name by two hyphens (`--`) (e.g., `block--modifier`, `block__element--modifier`).

### Benefits of BEM

*   **Modularity:** Blocks and elements are independent, making them reusable and easier to maintain.
*   **Clarity:** The naming convention clearly indicates the relationship between HTML and CSS, making it easier to understand the code.
*   **Scalability:** BEM helps manage large codebases by preventing naming collisions and reducing specificity issues.
*   **Collaboration:** Provides a consistent structure for teams to follow.

## Code Examples

### HTML Structure with BEM

```html
<header class="header">
  <nav class="menu">
    <ul class="menu__list">
      <li class="menu__item menu__item--active">
        <a href="#" class="menu__link">Home</a>
      </li>
      <li class="menu__item">
        <a href="#" class="menu__link">About</a>
      </li>
    </ul>
  </nav>
  <button class="button button--primary button--large">
    <span class="button__icon"></span>
    <span class="button__text">Click Me</span>
  </button>
</header>
```

### CSS with BEM

```css
/* Block */
.header {
  background-color: #f0f0f0;
  padding: 20px;
}

.menu {
  /* ... */
}

.button {
  display: inline-flex;
  align-items: center;
  padding: 10px 15px;
  border: none;
  cursor: pointer;
}

/* Element */
.menu__list {
  list-style: none;
  margin: 0;
  padding: 0;
}

.menu__item {
  display: inline-block;
  margin-right: 10px;
}

.button__icon {
  width: 16px;
  height: 16px;
  margin-right: 5px;
  background-color: currentColor;
}

/* Modifier */
.menu__item--active {
  font-weight: bold;
  color: blue;
}

.button--primary {
  background-color: #007bff;
  color: white;
}

.button--large {
  padding: 15px 25px;
  font-size: 1.2em;
}
```

## Resources

*   **Official Site:** [BEM (Block Element Modifier)](http://getbem.com/introduction/)
*   **Article:** [CSS-Tricks - BEM 101](https://css-tricks.com/bem-101/)
*   **Video:** [BEM Crash Course - Kevin Powell](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
