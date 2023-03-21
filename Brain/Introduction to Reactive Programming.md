> [Source](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754)
> [Video source](https://app.egghead.io/playlists/introduction-to-reactive-programming-using-rxjs-5)

## Intro

The hardest part of this is `thinking in reactive`

Its alot about letting go of old imperative and stateful habits of typical programming, and forcing your brain to work in a different paradigm.

## What is Reactive Programming?

> Reactive programming is programming with asynchronous data streams

- Event busses or click events are really an asynchronous event stream
- Where you can observe and trigger side effects.

> Reactive is triggering side effects basing on conditions of the event stream

- Everything can be a stream: variables, user input, props, caches, data structures
- `e.g` twitter feed would be a data stream in the same fashion that click events are
- all streams can be ==listened== to and ==react accordingly==

With this, most of the time you are given an incredible ==toolbox of functions== to combine, create, filter any of those streams.
- Functional magic
- A stream can be an input to another one
- Multiple stream can be used as input to another
- Merge two stream
- Filter streams to get specific info
- Map data from one stream to another

### Reactive Streams
==**Streams** are central to Reactive==, for example a button click event
![[Pasted image 20230129154638.png]]
**A stream** is a sequence of ==ongoing events ordered in time==
Streams can emit:
- A value (of a type)
- An Error
- A "Completed" signal
A "completed" signal only take place when the stream is closed.

These emitted evens are only captured `asynchronously` by defining a function that will 
- execute when a value is emitted
- another function that executes when there is an error
- another function when completed is emitted
Sometimes, `error` and `completed` can be skipped and just focus on defining functions for emitted values

> This is called ==subscribing==

The defined functions are `Observers`
The stream is the subject or `Observables` being observed

> [[Observer pattern]] This is essentially the [[Observer Design Pattern]]
> #TODO organizes and note more on this pattern

### Stream diagrams
Alternate to diagrams of streams drawn in ascii used throughout the tutorial
```
--a---b-c---d---X---|->

a, b, c, d are emitted values
X is an error
| is the 'completed' signal
---> is the timeline
```
### Stream example
> we are going to create new click event streams out of the original click event stream

- First make a counter stream that indicates how many time a button was clicked
In common Reactive libraries, each stream has many functions attached to it (`map`, `filter`, `scan`, ...)
e.g calling `clickStream.map(f)`
- this returns a `new stream` based on the click stream
- this does not modify the original `clickStream`
> streams are `immutable`

This allows us to chain functions like `clickStream.map(f).scan(g)`
```
clickStream:   ---c----c--c----c------c-->
               vvvvv map(c becomes 1) vvvv
               ---1----1--1----1------1-->
               vvvvvvvvv scan(+) vvvvvvvvv
counterStream: ---1----2--3----4------5-->
```
- `map(f)` replaces (into a new stream) each emitted value base on function `f`
	- this case replaces to 1 each click
- `scan(g)` aggregates all previous value on stream.
	- producing `x = g(accumulated, current)` - seems like reduce
	- where `g` simply add the function in the this example
- `counterStream` emits the total number of click whenever a click happens

Showing the ==REAL POWER== of reactive. let say if you want to have a stream of `double click` events
- making it more interesting, you want it to also consider `multiple clicks` as double
This will be extremely complex to do in the regular imperative - stateful fashion

This is very simple as Reactive with 4 lines of code
```js
var multiClickStream = clickStream
  .buffer(() => clickStream.throttle(250))
  .map((list) => list.length)
  .filter((x) => x >= 2);
```

![[Pasted image 20230129171300.png]]
- first aggregate the click in the stream into list, when ever 250ms of "event silence"
- next map each value list into a value showing the length of the list
- then filter length value >= 2
- we can then `subscribe` to it to react accordingly

---
## Why RP?
- RP raises the level of abstraction of your code so you can focus on the interdependence of events that define the business logic
- Freeing you from constantly fiddling with large amount of implementation detail
> Code in RP will likely more concise 
> OK ?? even though it is a pain to dissect it right now

- The pros is more noticeable in modern webapps and mobile apps that are highly interactable with multiple events reacting to data events
- Majority of classic webpages was mostly submitting a massive form, then performing simple rendering to front end.
- Current apps needs to be more ==real time==
	- modifying a single field can trigger a save to backend
	- "likes" to content can be reflected in real time to other connected user...

> "modern" apps have an abundancy in real-time events of every kind that enable a highly interactive experience to the user

---
## Thinking in RP
OK lets see RP implementation un the real world example with a step-by-step guide on ==how to think in RP==
By the end of the tutorial, we would have produce real functioning code while knowing why we did each thing.

> Tutorial using
> JS and RxJS
> NOTE: doc is incredibly old, while programming syntaxes has evolved over timek
> Its concepts are still applicable to current day

---
## Implementing a "who to follow" suggestion box
In the twitter UI, there is an element suggesting accounts to follow
![[687474703a2f2f692e696d6775722e636f6d2f65416c4e62306a2e706e67.png]]
We are focusing imitating its core features:
- on startup, load account data from API and display 3 suggestions
- on `refresh` button click, loads 3 other accounts suggestions into 3 rows
- on `x` on an account row, clear only that account and display another
- each row display the accounts information

> Twitter closes API for unauthorized public, lets build UI for following people on github. [github api for getting users](https://docs.github.com/en/rest/users?apiVersion=2022-11-28#get-all-users)

---
## Request and Response
OK so how to approach this with `Rx`
> Remember (almost) everything can be a stream

Starting with the easiest feature `Load 3 accounts data from the API`
Simply
1. doing a request for data
2. getting response
3. rendering the response

lets go ahead to represent our request as a `data stream`
It will be a stream with only 1 emitted value ==the request==
> For now lets assume there is only 1 request, we will deal with ==multiple== requests later

This is a stream of URLs we want to request.
When ever a request happens it tells us 2 things
- `When` the request should be executed is ==when== the event is emitted (location of `a`)
- `What` should be requested is the value emitted `a`
```
--a------|->
Where a is the string 'https://api.github.com/users'
```

The official term for a stream is `Observable` for the fact a stream can be observed
```js
// simple stream with a single value
var requestStream = Rx.Observable.just('https://api.github.com/users');
```
This is only a stream of strings with no operations.
So to make something happens when a ==value is emitted==, we `subscribe` to the stream
```js
requestStream.subscribe(function(requestUrl) {
  // execute the request
  var responseStream = Rx.Observable.create(function (observer) {
    jQuery.getJSON(requestUrl)
    .done(function(response) { observer.onNext(response); })
    .fail(function(jqXHR, status, error) { observer.onError(error); })
    .always(function() { observer.onCompleted(); });
  });
  
  responseStream.subscribe(function(response) {
    // do something with the response
  });
}
```
Because Rx now is dealing with an ==asynchronous== data stream.
The response for that request be a stream containing data could ==arrive at some other time in the future==

`Rx.Observable.create()` here is creating a custom stream by informing each ==observer/subscriber== about 
- data events `onNext()`
- errors `onError()`
> This means a Promise is an Observable

You can convert a `Promise` to an `Observable`. Lets use that
A `Promise` is simply an `Observable` with ==one single emitted value==
`Rx` streams go beyond promises by allowing many returned values.

OK so notice that we have one `subscribe()` inside another
> Callback hell

And `responseStream` is dependent on `requestStream`.
As mentioned before, there are "simple mechanisms" in `Rx` for transforming/creating new streams out of other so we should be doing that

### Observable `map()` 
fundamental function `map(f)` takes value of stream A and apply `f()` on it, producing values on stream B
So here we are essentially mapping request Urls to response Promises (disguising as streams)

```js
var responseMetaStream = requestStream.map((requestUrl) => {
	return Rx.Observable.fromPromise(jQuery.getJSON(requestUrl));
})
```

this `metaStream` (stream of Streams)
this is a stream where each value is another stream.
think of it as a `pointer` 
- each emitted value is a pointer to another stream.
- e.g each request URL is mapped a pointer to the promise stream containing the corresponding response
![[687474703a2f2f692e696d6775722e636f6d2f48486e6d6c61632e706e67.png]]

`metastream` for responses looks confusing and doesnt seem useful
We only want a simple stream of responses, where each emitted value is JSON object, not `Promise` of JSON

> Introducing `flatMap`
> A version of `map` that `flattens` metastream by emitting on the "trunk" stream every thing that will be emitted on "branch" stream

```js
var responseStream = requestStream
	.flatMap(reqUrl => {
		return Rx.Observable.fromPromise(jQuery.getJSON(requestURL));
	});
```
![[687474703a2f2f692e696d6775722e636f6d2f4869337a4e7a4a2e706e67.png]]

Since responseStream is defined according to requestStream.
when there are more events later on requestStream, we will have the corresponding response events happening on responseStream as expected
```
requestStream:  --a-----b--c------------|->
responseStream: -----A--------B-----C---|->

(lowercase is a request, uppercase is its response)
```

our final code would look like
```js
var reqStream = Rx.Observable.just('https://api.github.com/users');

var resStream = reqStream
	.flatMap(reqUrl => {
		return Rx.Observable.just(jQuery.getJSON(reqUrl));
	});

resStream.subscribe(res => {
	// render res to DOM
})
```

#todo review this section from the top

---
## The refresh button

## Modelling the 3 suggestions with streams

## Closing a suggestion and using cached responses

## Reactive Programming summary

![[Introduction to Reactive Programminvg]]
