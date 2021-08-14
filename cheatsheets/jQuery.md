# JQuery

[JQuery Documentation](https://learn.jquery.com/)

## Why use JQuery?

* **Browser Incompatibility:** Allows us to not worry about cross browser compatibility issues.
* **Productivity:** Makes us more productive developers. Their motto is *"write less, do more"*
* **Satisfaction:** Many devs consider using jQuery to be more fun than plan javascript.

Today, new tools like React have resulted in a decline in jQuery usage, but we still want it on our resume.

## What can jQuery do?

* Manipulate DOM elements with ease
* Perform simple animations
* Make event bindings more powerful
* Communicate with servers via AJAX

### They *jQuery* Function aka - $()

The jQuery function provides different functionality - depending upon what we pass to it.

The function $() is actually a shorthand alias for a function named jQuery().

### Using $() to Select Elements

To select elements, we pass $()a string argument that represents a CSS3 selector, just like we did using querySelector& querySelectorAll. jQuery also has some non-standard selectors of its own.

Here is a nice summary of the ways we can select elements using the jQuery function:

<img src="https://i.imgur.com/AqB9VL3.jpg">  
<br></br>

To select elements by the type of the element, use the name of the tag, just like CSS. This would select all 
`<h1>tags: $('h1')`

All CSS3 selectors rules apply. For example, this is how you could select just the first li tag using the **:first-childpsuedo** class selector
**$('li:first-child')**

### jQuery Object Structure
Note the naming convention for variables used to hold a jQuery object is to start the name with a `$`.

The returned object is a special jQuery object with extra functionality added to it.

```js
// Set a var to reference a raw DOM element
var li = $li[0];

// Bummer, no super powers
li.fadeOut(); // causes an error

// Turn it into a jQuery object with super powers!
var $el = $(li);
$el.fadeOut();  // see you later alligator
// Example using chaining 
$(li).fadeIn();  // back so soon?

// More big fun...
$el.hide();
$el.show();
$el.toggle();
// A callback can be provided too!
$el.toggle(function() {
  console.log('done being toggled!');
});
```

### Iterating Elements in a jQuery Object

jQuery provides the **each** method that can be used to iterate over each raw DOM element:

```js
$('li').each(function(idx) {
  console.log( idx + ': ' + this.innerHTML );
});
```

Additionally, jQuery has set the  ***this*** keyword to point to the iteration's current native DOM element.

### JQuery `eq()` Method

The `eq()` method can be used to access an index in the array of DOM elements like we did using square brackets. However, `eq()` automatically wraps the DOM element in a jQuery object with all of the magic:

```js
var $li = $('li');

// Fade out just the second <li>
$li.eq(1).fadeOut();
```

### The `html()` Method

jQuery's `html()` method is used for both geting & setting a DOM element's innerHTML property.

Here's out to change the text of the "inner" `<div>` from "Inner div" to "jQuery Rocks!"

```js
$('#inner').html('jQuery Rocks!');
```

When using a setter to modify the DOM, the change applies to all elements in the jQuery set. For example:

```js
// Change the content of all <li>'s
$('li').html('Hello SEI');
```

Many jQuery methods are designed to both **get** and **set** data on an element. The methods behavior depends on the arguments passed to it.

### The `css()` Method

The `css()` method is used to get and set the CSS properties of elements.

Here's how we can change the colorand font-weighton all of the \<li> elements:

```js
$('li').css( { color: 'green', 'font-weight': 'bold' } );
```

Use normalized names (camelCase) to avoid passing keys as strings:

```js
$('li').css( { color: 'green', fontWeight: 'bold' } );
```

The `css()` method also has a signature for setting a single CSS property

```js
$('p').css('font-size', '30px');
```

### Method Chaining

Each jQuery method, when used as a setter, returns the updated jQuery object. This allows us to "chain" methods like this:

```js
// Change our <p> tag's content and color
$('p').html('Awesome things jQuery can do:').css('background-color', 'peachpuff');
```

### Handy Methods

* `addClass()` - add a CSS class
* `removeClass()` - remove a CSS class
* `hasClass()` - test if an element has a class
* `toggleClass()` - toggle a css class

* `attr()` - add/modify the attributes of an element
* `removeAttr()` - removes an attribute
