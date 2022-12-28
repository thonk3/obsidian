> [RxJs Primer](https://www.learnrxjs.io/learn-rxjs/concepts/rxjs-primer)

## Observable

- represents a **stream** / source of data that arrive over time.
- Can form `Observables` from anything, the most common is `events`
	- mouse move
	- button click
	- text input
	- route change
- easiest way to create an observable is built-in creation functions
```js
// fromEvent example
import { fromEvent } from 'rxjs';

const button = document.getElementById('myButton');
const myObservable = fromEvent(button, 'click');
```
- So now the observable is there but its not doing anything as
	- `Observable` are cold
	- do not activate a producer (wiring up an event listener)
	- untill there is a `subscription`

## Subsciption

> `observables` are like stream of water ready to be tapped 
> some one needs to turn the handle
> Thats the role of the `subscriber`
- `subscription` set everything in motion
- to create one, call the `subscribe` method on the `observer`
	- now you can describe how to program reactively to each event
```js
// for now lets just log the event
import { fromEvent } from 'rxjs';

const button = document.getElementById('myButton');
const myObservable = fromEvent(button, 'click');
const subscription = myObservable.subscribe(event => console.log(event));
```
In this example calling `myObservable.subscribe()` will
1. set up event listener on the button for click events
2. call the call back function passed in `subscribe` on each click event
3. return a `subscription` object with an `unsubscribe` which contains cleanup logic (removing appropriate event listeners)

Subscribe method also accepts an object map to handle in case of error or completion.
- wont be as used as much as providing a call back
- useful to know
```js
// instead of a function, we will pass an object with next, error, and complete methods
const subscription = myObservable.subscribe({
  // on successful emissions
  next: event => console.log(event),
  // on errors
  error: error => console.log(error),
  // called once on completion
  complete: () => console.log('complete!')
});
```

NOTE: each subscription creates a new execution context
- if an `observer` is `subscribed` a 2nd time, it will create a new event listener
```js
const subscription = myObservable.subscribe(event => console.log(event));
const secondSubscription = myObservable.subscribe(event => console.log(event));

// clean up with unsubscribe
subscription.unsubscribe();
secondSubscription.unsubscribe();
```

By default
- subsciption creates a one-on-one, one sided convo between observable and observer
- this is `unicasting`
- like the boss `observable` yell `emit` at staff `observer` for a bad PR
- In the context where there is many `observers` this is called `multicasting`

> While working on a stream of events its nice.
> Its only so useful on its own
> 
> what makes RxJs the "lodash for events" are its `Operators`

## Operators
`Operators` are ways to manipulate values from a source, returning an `observable` of the transformed values
- Many are similar to JS arrays methods
```js
import { of } from 'rxjs';
import { map, filter } from 'rxjs/operators';
/*
 *  'of' allows you to deliver values in a sequence
 *  In this case, it will emit 1,2,3,4,5 in order.
 */
const dataSource = of(1, 2, 3, 4, 5);

const subscription = dataSource
  .pipe(map(value => value + 1))
  .subscribe(value => console.log(value))
  // log: 2, 3, 4, 5, 6
  .pipe(filter(value => value >= 4))
  .subscribe(value => console.log(value));
  // log: 4, 5 ,6
```
 In any case, if there is a problem needs to be solved, there exist an operator for that
 
> Another thing you may notice in the above examples, `operators` are called within `pipe` functions

## Pipe
the `pipe` function is the assembly line from the observable datasource through the operators.

Just as an Assembly line, the Data Source can pass through a `pipe` line of `operators`,
where data is manipulated as the user see fit

```js
// observable of values from a text box, pipe chains operators together
inputValue.pipe(
  debounceTime(200),         // wait for a 200ms pause
  distinctUntilChanged(),    // if the value is the same, ignore
  // if an updated value comes through while request is still active cancel previous request and 'switch' to new observable
  switchMap(searchTerm => typeaheadApi.search(searchTerm))
)
  .subscribe(results => {    // create a subscription
  // update the dom
  });
```

## Operators Grouped by Categories

### Creation Operators

### Combination Operators

### Error Handling Operators

### Filtering Operators

### Multicasting Operators

### Transformation Operators

## Operators have Common Behaviors

## Other Smilarities between operators

## What to do with all this?

## O boy

---
#angular