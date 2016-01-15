
> You may have heard of functional reactive programming. Here’s the gist: FRP uses functional utilities like map, filter, and reduce to create and process data flows which propagate changes through the system: hence, reactive. When input x changes, output y updates automatically in response. https://medium.com/javascript-scene/the-two-pillars-of-javascript-pt-2-functional-programming-a63aa53a41a4#.emch3u1ay

```javascript
$('#cats-btn').click(function () {  
  if(timeDiff < 500) {  return; }
  getDataFromServer('cats');
  // save time
});
function getDataFromServer(type) {  
  $.ajax(URL + type).done(function (cats) {
    renderUI(cats.map(formatCats));
  });
}
function formatCats(cat) {  
  return { name: 'Hello ' + cat.name }
}
function renderUI(data) {  
  UI.render(data);
}
```

becomes:

```javascript
_('click', $('#cats-btn'))  
  .throttle(500)    // can be fired once in every 500ms 
  .pipe(getDataFromServer)
  .map(formatCats)
  .pipe(UI.render);
```
Source: https://blog.risingstack.com/functional-reactive-programming-with-the-power-of-nodejs-streams/

"Are we talking about promises? Not exactly. Promise is a tool, FRP is a concept."
Source: https://blog.risingstack.com/functional-reactive-programming-with-the-power-of-nodejs-streams/

> One question you may ask yourself is why RxJS? What about Promises? Promises are good for solving asynchronous operations such as querying a service with an XMLHttpRequest, where the expected behavior is one value and then completion. Reactive Extensions for JavaScript unify both the world of Promises, callbacks as well as evented data such as DOM Input, Web Workers, and Web Sockets. Unifying these concepts enables rich composition. https://github.com/Reactive-Extensions/RxJS

Observables take async code (like events) and turn them into a collection. Which you can perform set operations on. There is a temporal property to items in the collection, meaning we can do time related operations like getting the latest value, throttling.

Observables "are iterators turned inside out", while you have to keep calling `next()` on an iterator to do something with the next value, observables call a next function when they get a value.

```javascript
myObservable.subscribe(success, error, complete);
```

Creating an Observable from a websocket conection event
```javascript
var connectionObservable = rx.Observable.create(observer => {
    socketServer.on('connection', (socket) => {
        observer.onNext(socket);
        // observer.onCompleted();  //signals the stream has completed (no more data)
    });

    //return cleanup function
    return () => {};
});
```
