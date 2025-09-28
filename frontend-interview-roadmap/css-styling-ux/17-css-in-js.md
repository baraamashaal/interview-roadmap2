
# 17. CSS-in-JS

## Quick Revision

**CSS-in-JS** is a styling technique where CSS is authored directly within JavaScript files, rather than in separate `.css` files. This approach aims to bring the benefits of component-based development to styling, offering features like component-scoped styles, dynamic styling, and easier maintenance.

Popular CSS-in-JS libraries include:

*   **Styled Components:** Uses tagged template literals to write CSS directly in JavaScript.
*   **Emotion:** A high-performance, flexible CSS-in-JS library.
*   **Styled JSX:** Built into Next.js for component-scoped styles.

## Detailed Explanation

Traditionally, CSS and JavaScript have been kept in separate files. While this separation of concerns has its benefits, it can lead to challenges in large, component-driven applications:

*   **Global Scope:** CSS is global by default, leading to naming conflicts and unintended style overrides.
*   **Dead Code Elimination:** Difficult to remove unused styles.
*   **Dynamic Styling:** Can be cumbersome to apply dynamic styles based on component state.

CSS-in-JS aims to solve these problems by co-locating styles with their components.

### Key Benefits

*   **Component-Scoped Styles:** Styles are automatically scoped to the component, preventing naming collisions and ensuring styles don't leak to other parts of the application.
*   **Dynamic Styling:** Easily apply styles based on component props or state.
*   **Easier Maintenance:** Styles are defined alongside the component, making it easier to understand and maintain.
*   **Dead Code Elimination:** Unused styles can be automatically removed by bundlers.
*   **Theming:** Simplifies theme management by using JavaScript variables for colors, fonts, etc.

### How it Works (Styled Components Example)

Styled Components uses tagged template literals to define styles. It generates unique class names for your components at runtime, ensuring that styles are scoped.

```jsx
import styled from 'styled-components';

const Button = styled.button`
  background-color: ${props => props.primary ? 'blue' : 'gray'};
  color: white;
  padding: 10px 15px;
  border-radius: 5px;

  &:hover {
    opacity: 0.8;
  }
`;

function MyComponent() {
  return (
    <div>
      <Button primary>Primary Button</Button>
      <Button>Secondary Button</Button>
    </div>
  );
}
```

## Code Examples

### Styled Components

```jsx
import React, { useState } from 'react';
import styled from 'styled-components';

const StyledButton = styled.button`
  background-color: ${props => (props.$primary ? '#007bff' : '#6c757d')};
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  margin: 5px;

  &:hover {
    opacity: 0.9;
  }
`;

const Container = styled.div`
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #f0f2f5;
`;

function App() {
  const [isPrimary, setIsPrimary] = useState(true);

  return (
    <Container>
      <StyledButton $primary={isPrimary} onClick={() => setIsPrimary(!isPrimary)}>
        {isPrimary ? 'Primary' : 'Secondary'} Button
      </StyledButton>
    </Container>
  );
}

export default App;
```

### Emotion (using `css` prop)

```jsx
import React from 'react';
import { css } from '@emotion/react';

const color = 'hotpink';

function App() {
  return (
    <div
      css={css`
        padding: 32px;
        background-color: hotpink;
        font-size: 24px;
        border-radius: 4px;
        &:hover {
          color: ${color};
        }
      `}
    >
      Hover to change color
    </div>
  );
}

export default App;
```

## Considerations

*   **Runtime Overhead:** CSS-in-JS libraries add a small runtime overhead, as styles are generated and injected into the DOM at runtime.
*   **Learning Curve:** Can have a steeper learning curve compared to traditional CSS.
*   **Server-Side Rendering:** Requires specific configuration for SSR to avoid FOUC.

## Resources

*   **Article:** [CSS-in-JS: The Good, The Bad, and The Ugly](https://www.freecodecamp.org/news/css-in-js-the-good-the-bad-and-the-ugly/)
*   **Library:** [Styled Components](https://styled-components.com/)
*   **Library:** [Emotion](https://emotion.sh/docs/introduction)
*   **Video:** [CSS-in-JS Explained - Fireship](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
