# HTML

HTML stands for hyper text markup language. It is a structural standard for displaying information on the web.

## DOCTYPE

DOCTYPE is an abbreviation for **Document Type**. A **DOCTYPE** is always associated to a __DTD__, for __Document Type Definition__.

A DTD specifies how documents of a certain type should be structured, ex by saying a button can contain a span but not a div. 

A DOCTYPE tells the browser what DTD the document supposedly respects, ex this document respects the HTML DTD.

For webpages, the DOCTYPE declaration is required, and tells user agents (browsers) what version of the HTML specifications the document respects. Once a user agent has recognizzed a correct DOCTYPE, it will trigger the __no-quirks mode__, matching this DOCTYPE for reading the document. If the user agent doesn't recognize a correct DOCTYPE, it will trigger the __quirks mode__.

Proper DOCTYPE declaration for the HTML5 standard is `<!DOCTYPE html>`

## Serving multiple languages

When a request is sent to a server, the requesting agent usually specifies language preferences in the __Accept-Language__ header. The document returned with reflect the requested language in the html property, _lang_. Ex `<html lang="en">...</html>`

## Considerations for multilingual websites

* Use the `lang` property in the HTML head tag
* Allowing easy access to switching the currently displayed language.
* Avoid images with text. This gets out of hand when duplicating the images across languages.
* Text can be longer / shorter in different languages. Make sure this won't negatively affect the format.
* Consider color usage as they are perceived differently across cultures.
* Formatting dates + currencies
* Do not concatenate translated strings, as things like nouns belong in different locations of the sentence in different languages.
* Support RTL and LTR reading languages.
* Include the locale in the path - en_US, zh_CN etc. 

## Building blocks of HTML5

* Semantics - allows more precise description of the content
* Connectivity - allows new and innovative ways to communicate with the server
* Offline + Storage - Allows webpages to store data on client side locally and operate offline more efficiently
* Multimedia - Making video and audio first-class citizens in the Open Web
* 2D/3D graphics and effects - Wider spectrum of presentation options
* Performance and integration - Providing more speed optimizations and better usage of computer hardware.
* Device access - Allows for using various input and output devices
* Styling - authors write more sophisticated themes

## Cookies, sessionStorage & localStorage

All of these are technologies to store string values in a key-value storage mechanism.

| | cookie | localStorage | sessionStorage|
|---|------|--------|---------|
|Initiator|Client or server. Server can use Set-Cookie header. | Client | Client|
|Expiry|Manually Set| Forever | On tab close|
|Persistent across browser sessions|Depends on whether expiration is set| Yes|No|
|Sent to server with every HTTP request|Cookies are automatically being sent via `Cookie` header|No|No|
|Capacity (per domain)|4kb|5MB|5MB|
|Accessibility|Any window|Any window|Same tab|

When a user clears their browsing data, usually all three of these mechanisms are wiped out.

## Script tag options

`<script>` - HTML parsing is blocked, the script is fetched and executed immediately, HTML parsing resumes after the script is executed

`<script async>` - The script will be fetched in parallel to HTML parsing and executed as soon as it is available (possibly before HTML parsing is complete). This is best used when the script is independent of any other scrips on the page, such as for analytics.

`<script defer>` - The script is fetched in parallel to HTML parsing and executed when the page has finished parsing. If multiple deferred scripts exist, they are executed in the order they were presented on the document. Useful for scripts relying on a fully-parsed DOM, however must not contain any `document.write` statements.

`async` and `defer` attributes are ignored for scripts that have no `src` attribute.

## Placement of `links` and `scripts`

`<link>` tags being placed in the `<head>` is part of proper specification in building an optimized website. Basically you want to get your CSS loading alongside the HTML so that the browser doesn't repaint content if the styling changes by having a link to a css file at the end of the document. This can cause flashes of unstyled content (FOUC), which is not a good look.

The convention is to place `<script>` tags just before the `<body>` tag. The script tags block html parsing however, which can slow down the parsing / rendering process. If this is happening it might be best to move the `<script>` tag to the end or slap a defer or async on it. 

## Progressive Rendering

Progressive rendering is the techniques used to improve performance and reduce perceived load time. 

Examples include:

- Lazy loading images (javascript is used to load it when the user scrolls to where it should be)
- Prioritizing visible content (above-the-fold rendering) - Include only the minimum css/content/scripts necessary for the amount of page that would be rendered first to display as quickly as possible. Then load other assets behind the scenes.

## `srcset` attribute on image tags

This attribute should be used when you want to server different images to users depending on their device display width.

For example:
`<img srcset="small.jpg 500w, medium.jpg 1000w, large.jpg 2000w" src="..." alt=""> ` tells the browser to display the small, medium or large image depending on the client's resolution. This can save memory by not forcing a small device to load a large image that it can even utilize the extra resolution. 