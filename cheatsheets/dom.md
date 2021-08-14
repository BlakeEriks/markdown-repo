# The DOM (Document Object Model)

### Select a single element by its *id*
```
let titleEl = document.getElementById('title');
console.log(titleEl);
```

### Select a single element using a CSS selector

* The selector argument is a string that follows the rules of regular CSS3 selectors.
* Use a **#** to target an id, ex: `document.querySelector('#title');`
* Use a **.** to target a CSS class, ex: `document.querySelector('.title');`

### Element properties
* innerHTML: used to retrieve/set content as HTML
* textContent: Used to retrieve/set content as plain text

### Element Functions
* getAttribute(name)
* setAttribute(name, value)
* hasAttribute(name)

### Events

DOM events are the bedrock of interactivity on web pages.

Events enable us to implement event-driven programming, such that much of our code runs in response to events being triggered during run-time.

Event examples:
* Mouse move or clicks
* User presses a key
* When form is submitted
* Page has finished loading or has been resized

**Event Listeners** are functions, more specifically, callback functions, that are called when an event fires.  

They are also referred to as *event handlers*.

Common syntax for registering an event listener for a given event:

`element.addEventListener(<event-name>, <callback>, <use-capture>);`












