
## 1.1 motivation
- State management in angular apps
When starting, you won't be focusing on state management, but as the application grow in complexity.
One of the hardest task during development would be updating and synchronizing states. And it is all over the place during modern web apps
- `view state` whats displayed
- `client state` the data in the application. the i/o
- `browser state` whats the ur / the browser storage / the network
- `server state` whats persisted in the database
These are the standard state but
> [!Info] Basically
> anything can change within the context of your app may called the state

Angular already has a kind of built in state mangement technique `Components`
They act as bridge between client and view state as they render/ receive data via template binding.
Also, template components are classes that natrually encapsulate state through instance properties.
Components arnt simply responsible for view suncronization but are also state containers.
And data is passable via `@Input` and `@Output` bindings between parent and child components. Consequently the state will flow along the view heirachy.

This gets very hard when somestate has to be shared between distant components in ternm of the view heirachy.
Forcing you to put alot of the state higher up in the component (or root) while other components forward data that they may not need (unecessary code)
This could end up with many "hybrid" state containers
![[Pasted image 20230218130933.png]]

Angular offers `services` as a solution to this. The class instance lives outside of the view heirachy and can be `injected` to any components - perfect for sharing state.
But when working with Angular, `services` already enable us to build dedicated state containers, while components can focus on rendering views and triggering state change back in a service.

The centerpiece of NgRx is much more than a state container service.

Solving sharing data is just the first step, the next problem is its hard to keep track of when state change.
Especially if it can be mutated from many places within the application.
This is when angular developers reach for observable streams and immutability.
Components then listen to a stream of subsequent states while they send off commands via `service` methods. This approach is often bases on rxjs `BehaviorSubject`

So we're introducint `Command Query Responsibility Segregation` (CQRS) pattern which provides unidirectional data flow.
There are now predefined ways in which state can change and we can besure that all consumers will be notified with change.
![[Pasted image 20230218135212.png]]

> Skip a bit to

`NgRx` solution:
replace commands with events and introduce an event-bus.
Instead of issuing commands to a specific service, its now broadcasting events ==globally== which each part of the state can react independently.

> This way, we have a single-source of truth for shared state

Levaraging a formalized solition like `NgRx` opens up a whole community where people speak the same state management language and create convinient development tools. You'll be able to:
- time travel through your applicaiton
- facilitate fast restarts based on data
- easily implements features like undo redo

> [!Note] Learning NGRX
> and its principles won't solve all your problems, but it will put a battle tested tool in your belt for approaching state management in modern software development

> more [ReThingking state in Angular Applications](https://www.youtube.com/watch?v=Azus3_CEkpw)

## 1.2 concepts and terminology
The service containing the global state is the `NgRx Store`.
It exposes the current state as an `RxJs` observable and accepts incomming events (`actions`)
When such `actions` are ==dispatched==, the store compute the next state based on incomming information based on attached information.
Subsequently, the computer state is pushed to all subscribed consumer throught the store observable.

### NgRx Terminology
- `state` single object representing the global application state.
	- usually defines an interface that specified what the state looks like in order to reference it in reducers and consumers.
	- you'll need an initial state that starts off your application state management with default values
- `action` unique event occurring in your application that is relevant to the global state management.
	- may lead reducers to producing a new state.
	- object distinguised by a type string anc may contain meta data about the underlying event
- `reducer` pure function that takes the current state and an action and turn returns the new state
- `store` the store manages the state by infoking all registered reducers when it registers an action.
	- at the same time, makes the sate accessible as a stream of values
- `selector` pure function retrieving certain parts of the state from the store, while optionally applying additional transformation
	- the re-computation of the transformation can be minimized through a process called memoization, where the cached results are returned as long as the input stays the same.
- `feature` set of one or more recuders optionally plus corresponding actions/effects/selectors/ representing a unit of state based functionality
- `effect` explicit definition of interaction between the state management and other (possibly asynchronous) units (storage) or operations (http requests)

## 1.3 NgRx is not just a store
- ngrx its more than its store solution

> you can read more on 
> - @ngrx/component
> - @ngrx/component-store

## 1.4 you might not need ngrx

> [!info] the **SHARI** principle
> ngrx might be for you if
> `S`hared - same state is used by multiple component and/or services
> `H`ydrated - state is (de-)serialized from a persistent storage
> `A`vailable - state is supposed to outlive a component or route
> `R`etrieved - state is provided by a possibly expensive side-effect (Http request) which should't run everytime you need the state
> `I`mpacted - state is impacted by events from various sources

---
next chapter [[NilsNgRx - 2 - Example app]]