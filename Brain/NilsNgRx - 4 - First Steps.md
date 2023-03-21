## Overview
A general overview of how everything fits together.

> State management with `NgRx` is a cycle without a single starting point.

Hence, lets jump into a simple example of a counter

> For now lets place all NgRx related code into store.ts

In order to request the counter increment, we define an action creator.
importing the helper function `createAction()` from `@ngrx/store` and pass a type(unique name) for the action

```ts
import { createAction } from '@ngrx/store';

export const increment = createAction("[counter] increment");
```

Last thing to do is define how the action is handled. `reducers`
This is done by importing the helper function `createReducer()`
- for the first arg - pass in the initial count of 0;
- for the second arg - pass the return value of another helper function `on()`
	- it creates a tiny reducer that will only handle the types of actions we specify. basically declare a state transition for a specific action.
	- reducer function we pass to `on()` will define how this transition compute the next state from the last one
```ts
import { on, createReducer } from '@ngrx/store'

export const reducer = createReducer(
  0,
  on(increment, state => state+1)
);
```

Now to connect the store setup with the actual application.
We need to define which part of the application state should be handled by the `countReducer`.
This is done by creating an object of type `ActionReducerMap` witha  generic parameter represents our type of state.
Such a map assign a slice of state(lhs) to a reducer(rhs).

Naturally the `countReducer` is going to compute the property of our `State` interface

```ts
import { ActionReducerMap } from '@ngrx/store'

export const reducers: ActionReducerMap<State> = {
  count: countReducer
}
```

> now go a head and ==register the reducer== by mapping with the store. (pass it to `forRoot()`)

As of here the setup is complete.
The only thing left to do is build a component that can display the current count trigger that can display the current count / trigger an increment

So lets create a `Counter` component
> refer to the code for sample, you know the syntax for this

Inside component class we define an observable `count$` (this is just a notation) (pluralization - finish notation)

constructor declares a parameter to inject the NgRxStore.
the `Store` service is an observable emitting everytime a new application state is reduced.
calling `select()` allows us to only look at a specific slice of the whole state, by passing a projecting function.
Its the RxJs operator `map()` and `distinctUntillChanged()` combined, providing an observable of distict state slices.

The store also provides a function for dispatching actions.
We use it to provide a method for incrementing our counter when invokeing the action creator defined earlier.

In the view template.
bind the counter state to the view through `AsyncPipe` 
bind the click event to the increment method

---

The following show how simple it is to add new business logic to the current ngrx setup
adding `multiplication`

1. add a new `createAction()` object with a new action string
This time add a 2nd argument `props()` to setup a payload of the action.
`props()` accepts a generic parameter that defines the shape of the action payload.
```ts
export const mult = createAction(
	'mult action', 
	props<{ factor: number }>()
)
```
2. add a function to dispatch the new action, while also passing in the arg for the payload
```ts
multiply(f: number) {
	this.store.dispatch(mult({ factor: parseInt(f) }));
}
```
3. bind the function into the template onClick
4. add another case into th existing reducer to handle `multiply`


---
next chapter [[NilsNgRx - 5 - Debugging]]