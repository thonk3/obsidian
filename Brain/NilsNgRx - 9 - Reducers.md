
> [!note] Reducers
> are like a funnel, the current state and action are dropped at the top,
> the next state comes out of the bottom, nothing else

- actions can be dispatched even if there are no reducers
	- this is for actions can also trigger effects
- most of the time, one reducers reacts to at least one action type.
- possible for many reducers to handle the same action type.
	- as every reducer will recieve every dispatched action.

Reducers produces the next state by returning a new object that implements the next state interface.
- again states are immutable
- its crucial to create a new object to simplify change detection

> Eye spread operators op

- it only makes a ==shallow copy== of an object, so parts of the current state is also passed into the next state.

> lots of useful but known information maybe warrants a #review

## 9.1 Creating Reducers
Again using create functions.
Reducers are created by passing an ==initial state== and smaller state change functions to `createReducer()`.
- each individual state change function defined with `on()` to set one or more action type to the reducer.
- let you generate action specific state transition that benefit from strick type-checking.

When an action is dispatched
- ngrx iterate all of your state change functions and execute the ones that match based on action type
- If there are multiple matching actions, each will be executed in order
	- be, wary that it may hard to determine where is an error 
	- youll have to look in multiple places in order to understand what an action is doing to a single slice of state.

## 9.2 Registering Reducers

> [!info]
> the next global state is produced by funelling state slices, through their corresponding reducers.
> All reducers will be called regardless if they handle the action or not.
> If there is no change, the state is returned as is

the store manages the state in a single objeect while each smaller slices are processed by designated reducers.
The global state will need to be formed by assembling the types of all sclices.

```ts
// index.ts
import { IssueState } from './issue/issue.state';

export interface RootState {
	issue: IssueState;
}
```

Then define a mapping from each state slice corresponding to a reducer using `ActionReducerMap`, parametrize with the type of the application state

```ts
// index.ts
import { ActionReducerMap } from '@ngrx/store';
import { issueReducer } from './issue/issue.reducer';

export const reducers: ActionReducerMap<RootState> = {
	issue: issueReducer
}
```

then pass that mapping variable `reducers` by importing `StoreModule.forRoot()`

That is essentially everything ngrx needs to kick-off state management for your application.
- Importing `StoreModule` like this will make `Store` avaliable for dependency injection.
- `forRoot` also accept a 2nd config param. alloing runtime checks notifying about unintended violation of immutability, serialization or action type uniqueness.
Registering reducers this way will initialize them directly at application startup.
Later on [[NilsNgRx - 12 - Reducers]] will look into registering additional reducers that can be lazy-loadde through feature modules.

## 9.3 Mutable APIs with immer.js

Introducing `immer.js` for an alternate way to ease the creation of state
- of course there is the spread operator but this is an alternative
```ts
const issue = {
	title: "using mutable api",
	description: "writing reducers",
	resolved: false
}

// return a new object
// doesnot mutate issue
const updatedIssue = produce(issue, (iss) => {
	iss.resolved = true;
});
```

> Of course this is not the only or the "best" way to do things
> Essentially it depends on your preference


## 9.4 Meta-Reducers

Meta Reducers are so called ==higher order reducers==
> Meta-reducers accepts an existing reducer, wrap some logic around it and return a new reducer.

> Reducer factories are also meta-reducers

> abit confusing still, maybe try to have a better understanding of the Factory pattern first then do some #review pg52

## 9.5 Error Handling

By definition, pure functions does not really allow to throw error.
What if it does

While you shouldn't throw errors inside a reducer, there is no guarantee that the code wont produce them.

There are things such as
- accessing undefined property
- getting type error parsing a string.
These errors ==buble up to Angular's global error handler==
Ngrx ==keeps the current sate and carries on like nothing happened==

General rule
Keep anything that might error out of the reducer.
Anything like parsing that is expected to error from input as a side effect. Either run it before dispatching an action or define a corresponding effect

If you want to ==enhance the stack trace== in some way or recover from unexpected error,
place a flag into the state, you might want to do so by wrapping your reducer in a try catch block