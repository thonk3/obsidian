## Using Observables to pass values

`Observables` provide support for passing messages between parts of your application.
- Very often used in `Angular`
- A technique for event handling, asynchronous programming, and hadnling multiple values

The `observer` pattern is a software design pattern where an `object` called the `subject`, maintains a list of its dependents or `observers`, and notifies them automatically of state changes.

> This pattern is similar but not identical to the [publish/subscribe design pattern](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern)

`Observables` are declarative
- you define a function for publishing values, but are not executed until a consumer subscibes to it
- `subscribed` consumer then receives notification until the function completes, or until they `unsubscribed`

`Observables` can deliver multiple values of any type(literals, messagee, or events, depending on the context).
The `API` for receiving values is the same whether the value is delivererd `synchronously` or `asynchronously`.
- the setup and teardown logic are both handled by the `observable`
- your app code only needs to wory about `subscribing` to consume values, and when done -> `unsubscribing`
Whether the stream was keystrokes, or an `HTTP` response, or an interval timer.
The interface for listening to values and stopping listening is the same

> Because of these advantages, `observables` are used extensively with `Angular` and for application development as well.

---
## Basic Usage and terms
As a publisher, you create an `Obserrvable` instance that defines a `subscriber function`.
This is the function that is executed when a consumer calls the `subscribe()` method.
- The subscriber function defines how to obtain or generate values or messages to be publish

To execute the observable you have created, and begin receiving notifications, you call its `subscribe()` method, passing an `observer`.
This is a `js object` that defines the handlers for the notifications you receive.
- The `subscribe()` call returns a `Subscription` object that contains an `unsubscribe()` method, which can be used to stop receiving notifications

Example code demonstrating **basic usage** model showing how an `Observable` could be used to provide geo-location updates.
```js
// Create an Observable that will start listening to geolocation updates
// when a consumer subscribes.
const locations = new Observable((observer) => {
  let watchId: number;

  // Simple geolocation API check provides values to publish
  if ('geolocation' in navigator) {
    watchId = navigator.geolocation.watchPosition(
	    (position: GeolocationPosition) => { observer.next(position);}, 
	    (error: GeolocationPositionError) => { observer.error(error);}
		);
  } else {
    observer.error('Geolocation not available');
  }

  // When the consumer unsubscribes, clean up data ready for next subscription.
  return {
    unsubscribe() {
      navigator.geolocation.clearWatch(watchId);
    }
  };
});

// Call subscribe() to start listening for updates.
const locationsSubscription = locations.subscribe({
  next(position) {
    console.log('Current Position: ', position);
  },
  error(msg) {
    console.log('Error Getting Location: ', msg);
  }
});

// Stop listening for location after 10 seconds
setTimeout(() => {
  locationsSubscription.unsubscribe();
}, 10000);
```

## Defining Observers
A `handler` for receiving `observable` notifications implements the `Observer` interface. It is an object that defines callback methods to handle 3 types of notifications an `observable` can send:

|Notification Type |Details|
|---|---|
|`next`|_Required._ A handler for each delivered value. Called `> = 0` times after execution starts. |
|`error`|_Optional._ A handler for error notification. An error halts execution of the observable instance. |
|`complete`|_Optional._ A handler for the execution-complete notification. Delayed values can continue to be delivererd to the next handler after execution is complete. |

An `observer` object can define any combination of these handlers.
If a notification handler is not supplied, the `observer` ignores notifications of that type.

## Subscribing
An `Observable` instance begins publishing values only when someone subscribes to it.
You subscribe by calling `subscribe()` method of the `observable` instance, passing an observer object to receives the notifications.

> To show how subscribing works, an `observable` needs to be created.
> There is a `constructor` that creates new instances.
> 
> But for illustration, there are some methods from the `RxJs` library that creates simple observables:

|Notification Type |Details|
|---|---|
|`of(...items)`|Returns an `Observable` instance that synchronously delivers the values provided as args|
|`from(iterable)`|Convers its args to an `Observable` instance. Commonly used to convert array to `observables`|

Example of creating and `subscribing` to a simple observable, with an observer that logs the received message to the console:

```js
// Create simple observable that emits three values
const myObservable = of(1, 2, 3);

// Create observer object
const myObserver = {
  next: (x: number) => console.log('Observer got a next value: ' + x),
  error: (err: Error) => console.error('Observer got an error: ' + err),
  complete: () => console.log('Observer got a complete notification'),
};

// Execute with the observer object
myObservable.subscribe(myObserver);

// Logs:
// Observer got a next value: 1
// Observer got a next value: 2
// Observer got a next value: 3
// Observer got a complete notification
```

Alternatively, the `subscribe()` method can accept callback function in-line, for `next`, `error`, and `complete` handlers.
Example, the following `subscribe()` call is the same as the one that specifies the predefined owner:
```js
myObservable.subscribe(
  x => console.log('Observer got a next value: ' + x),
  err => console.error('Observer got an error: ' + err),
  () => console.log('Observer got a complete notification')
);
```
In either case, a `next` handler is required, the `error` and `complete` are optional
> **NOTE**
> A `next()` function could receive, things like message strings / event objects/ numeric values/ structures, depending on context.
>
> In general, we refer to data published by an `observable` as a `stream`.
> Any type of value can be represented with an `observable`, and the values are published as `stream`

## Creating Observables
Use the `Observable` constructor to create an `observable` stream of any type.
The constructor takes takes as its arg the `subscriber function` to run when the observable's `subscribe()` method executes.
A subscriber function receives an `Observer` object, and can publish values to the observer's `next()` method.

Example, to create an observable similar to `of(1, 2, 3)` you can do something like this:
```js
// This function runs when subscribe() is called
function sequenceSubscriber(observer: Observer<number>) {
  // synchronously deliver 1, 2, and 3, then complete
  observer.next(1);
  observer.next(2);
  observer.next(3);
  observer.complete();

  // unsubscribe function doesn't need to do anything in this
  // because values are delivered synchronously
  return {unsubscribe() {}};
}

// Create a new Observable that will deliver the above sequence
const sequence = new Observable(sequenceSubscriber);

// execute the Observable and print the result of each notification
sequence.subscribe({
  next(num) { console.log(num); },
  complete() { console.log('Finished sequence'); }
});

// Logs:
// 1
// 2
// 3
// Finished sequence
```

Taking this example further, we can create an `observable` that publishes events. 
In here, the `subscriber` function is defined inline.
```js
function fromEvent<T extends keyof HTMLElementEventMap>(target: HTMLElement, eventName: T) {
  return new Observable<HTMLElementEventMap[T]>((observer) => {
    const handler = (e: HTMLElementEventMap[T]) => observer.next(e);

    // Add the event handler to the target
    target.addEventListener(eventName, handler);

    return () => {
      // Detach the event handler from the target
      target.removeEventListener(eventName, handler);
    };
  });
}
```

Now we can use this function to create an observable that publishes keydown events
```js
const ESC_CODE = 'Escape';
const nameInput = document.getElementById('name') as HTMLInputElement;

const subscription = fromEvent(nameInput, 'keydown').subscribe((e: KeyboardEvent) => {
  if (e.code === ESC_CODE) {
    nameInput.value = '';
  }
});
```

## Multicasting
A typical `Observable` creates a new, independent execution for each `subscribed` observer.
- When an observer subscribes, the `observable` wires up an event handler and deliver values to that `observer`.
- When a **second** observer subscribes, the `observable` wires up a new event handler and deliver values to that second observer in a separate execution.

SO, sometime instead of starting an independent execution for each `subscriber`, you want each subscription to get the same value - EVEN if values has already started emitting.
- This might be the case with something like an `observable` of clicks on the document object

`Multicasting` is broadcasting to a list of multiple `subscribers` in a single execution.
For `multicasting observables`,
- multiple listeners are not registered on the document
- BUT re-use the first listener and send values out to each subscriber.

When creating an `observable`, it should be determined how the `observer` is used and whether or not it should be multicasted

Example
```js
function sequenceSubscriber(observer: Observer<number>) {
  const seq = [1, 2, 3];
  let timeoutId: any;

  // Will run through an array of numbers, emitting one value
  // per second until it gets to the end of the array.
  function doInSequence(arr: number[], idx: number) {
    timeoutId = setTimeout(() => {
      observer.next(arr[idx]);
      if (idx === arr.length - 1) {
        observer.complete();
      } else {
        doInSequence(arr, ++idx);
      }
    }, 1000);
  }

  doInSequence(seq, 0);

  // Unsubscribe should clear the timeout to stop execution
  return {
    unsubscribe() {
      clearTimeout(timeoutId);
    }
  };
}

// Create a new Observable that will deliver the above sequence
const sequence = new Observable(sequenceSubscriber);

sequence.subscribe({
  next(num) { console.log(num); },
  complete() { console.log('Finished sequence'); }
});

// Logs:
// (at 1 second): 1
// (at 2 seconds): 2
// (at 3 seconds): 3
// (at 3 seconds): Finished sequence
```

> [more on the examples](https://angular.io/guide/observables#multicasting)

## Error handling

Because `observables` produces values asynchronously, `try/catch` will not effectively catch errors.

`errors` are handled by providing an `error` callback on the observer.
Producing an `error` also cause the observable to clean up `subscriptions` and stop producing values.

An observable can either produce values(calling the `next` call back), or it can complete, calling `complete` or `error` callback.

```js
myObservable.subscribe({
	next(num) { console.log(`Next num: ${num}`); },
	error(err) { console.log(`Received an error: ${err}`); },
})
```

> Error handling / Recovering from an error is covered more later on

