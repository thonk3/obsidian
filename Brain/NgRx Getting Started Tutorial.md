Lets start a new project with the simple default instalation

```shell
ng add @rxjs/store@latest
```

> [!Note] source 
> https://ngrx.io/guide/store

## Getting started tutorial
This is a simple counter application to demonstrate the basics of `ngrx/store`

initialise a new default angular app with `--no-strict` (my pref for now)

### setup
1. `counter.actions.ts`
describe counter actions to increase, decrease and reset the counter value
2. `counter.reducer.ts`
handle changes in the counter value based on provided actions
define what happens when an action is provided
3. `app.module.ts`
	- import the reducer and ngrx `StoreModule`
	- add `StoreModule` into the imports array containing an object for the `count` and `counterReducer` that is managing the state of the counter
	- `StoreModule.forRoot()` registers the global providers needed to access the `Store` through out the application
4. a `my-counter` component to implement/use `ngrx`
	- interesting how its using observable for 

> as always, quite a bit of overhead

### Game time
So after all the setup
Essentially all we need to do is to 
- **inject** the `store` into the `MyCounter` component
- **connect** the store's `count` state
- **implements** the click method to dispatch actions to the store

> Holy shit, what the fuck


## Summary
this whole tutorial covers
- Define `actions` to express events
- Define a `reducer` function to manage the state of counter
- Define the global state container that is available throughout the application

---
Up next [[NgRx walkthrough]]