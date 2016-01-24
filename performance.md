Notes from http://chimera.labs.oreilly.com/books/1230000000545/ch10.html#_hypertext_web_pages_and_web_applications
An HTTP 0.9 session consisted of a single document request, which was perfectly sufficient for delivery of hypertext: single document, one TCP connection, followed by connection close.

Page Load Time (PLT) - time to onload event in the browser, which is an event fired by the browser once the document and all of its dependent resources (JavaScript, images, etc.) have finished loading.

> The load event fires at the end of the document loading process. At this point, all of the objects in the document are in the DOM, and all the images, scripts, links and sub-frames have finished loading.
https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/onload

Not to be confused with `DOMContentLoaded`:
>The DOMContentLoaded event is fired when the initial HTML document has been completely loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading. A very different event - load - should be used only to detect a fully-loaded page. It is an incredibly popular mistake to use load where DOMContentLoaded would be much more appropriate, so be cautious.
https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded
