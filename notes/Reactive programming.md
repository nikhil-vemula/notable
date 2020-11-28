---
tags: [Notebooks/Learning]
title: Reactive programming
created: '2020-08-15T08:37:44.358Z'
modified: '2020-08-15T18:55:39.801Z'
---

# Reactive programming

* Streams are ubiquitous like  event stream, value streams etc.
* Streams are ongoing events in time, it can emit three different things a value, complete or error.
* We can have functions that can process the value that is emitted, similarly we can have function on complete and on error.

Observer: The functions are called as observers.
Observable or Subject: The stream that is observed.
Subscribing: The process of listening to the streams is called subscribing.

# Rxjs

## Observer

```js

var observable = Observable.create((observer: any) => {
    observer.next('Hey guys!');
});

observable.subscribe((x: any) => console.log(x));

```

## Subject

Three types :

* Behaviour subject : The last message from first subscriber is recieved by the second subscriber
* Replay subject: The last n messages from subscriber are replayed to next subscriber
* Async subject: The last message is send when observer calls complete

## Operators

Can be applied to the observable to get a new observable

```js
var mutiply10 = map((x: any) => x*10);
const multiplied10 = mutiply10(from([1, 2, 3]));
multiplied10.subscribe((x: any) => {
    console.log(x);
}); 
```

## References

* [https://xgrommx.github.io/rx-book/why_rx.html](https://xgrommx.github.io/rx-book/why_rx.html)
