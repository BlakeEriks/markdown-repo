# Server Side Rendering (SSR)

Instead of the client / user browser, the server runs the react code + scripts and renders code into html

Client-Side Rendering
* Loads index.html
* Loads JS bundle from server
* runs bundle
* displays app
* loads data

Server-Side Rendering
* Runs JS bundle
* loads data
* Creates HTML document
* Sends to client

Client side rendering is less strain on data, but slower UX

SSR has faster user experience and better SEO

SSR Caveats:

* Code using window or document in client logic won't work (its not running in the browser)
