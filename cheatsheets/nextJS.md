# NextJS

## Pages

Pages are a react component located in the /pages directory in a nextJS project. 

Dynamic routes function with the naming convention `/pages/page/[id].js`

Using this, `/pages/page/1` would map to this map.

## Pre-rendering

By default, nextJS prerenders the HTML for every page in the application. This can result in better performance and SEO (search engine optimization).

Each of these generated HTML pages are associated with the minimal amount of javascript in order to make the page interactive. Once the page is loaded by the browser, the javascript is run. This process is called ***hydration***

NextJS has two forms of pre-rendering:

* **Static Generation**: The HTML is generated at ***build time*** and is reused on each request.

* **Server-side generation**: The HTML is generated on each request.

NextJS lets you choose which type of rendering to use for each page. A NextJS app using both forms of rendering is considered a hybrid app.
