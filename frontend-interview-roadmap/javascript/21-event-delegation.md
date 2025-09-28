
# 21. Event Delegation in JavaScript

## Quick Revision

**Event delegation** is a technique for handling events in which you attach a single event listener to a parent element instead of attaching multiple event listeners to individual child elements. The parent element then listens for events that "bubble up" from its children.

This approach is more efficient, especially for a large number of child elements or for dynamically added elements.

## Detailed Explanation

Event delegation relies on the concept of **event bubbling**. When an event is triggered on an element, it first runs the event handlers on that element, then on its parent, and then all the way up the DOM tree.

By attaching an event listener to a parent element, you can listen for events that occur on its descendants. The `event.target` property can be used to identify the actual element that triggered the event.

### Advantages of Event Delegation

*   **Improved Performance:** Fewer event listeners mean less memory usage and better performance, especially for a large number of elements.
*   **Dynamic Elements:** You don't have to add and remove event listeners when you add or remove child elements. The parent event listener will automatically handle events for any new children.
*   **Simpler Code:** It can lead to cleaner and more maintainable code.

## Code Example

### Without Event Delegation

```html
<ul id="myList">
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
```

```javascript
const listItems = document.querySelectorAll('#myList li');

listItems.forEach(item => {
  item.addEventListener('click', () => {
    console.log('Clicked on:', item.textContent);
  });
});
```

This approach has a few problems:
*   It requires adding an event listener to every `<li>` element.
*   If you add a new `<li>` to the list, you have to remember to add an event listener to it.

### With Event Delegation

```javascript
const list = document.getElementById('myList');

list.addEventListener('click', (event) => {
  if (event.target.tagName === 'LI') {
    console.log('Clicked on:', event.target.textContent);
  }
});
```

In this example, we attach a single event listener to the `<ul>` element. When a `<li>` is clicked, the event bubbles up to the `<ul>`, and our event listener is triggered. We then check if the `event.target` (the element that was actually clicked) is an `<li>` element before executing our code.

## Resources

*   **Article:** [MDN - Event delegation](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_delegation)
*   **Article:** [JavaScript Event Delegation](https://javascript.info/event-delegation)
*   **Video:** [Event Delegation - Beau teaches JavaScript](https://www.youtube.com/watch?v=3KJI1WZGDrk)
