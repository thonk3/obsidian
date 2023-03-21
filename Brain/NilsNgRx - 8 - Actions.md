
> [!info] action represent unique events occurring in your application
> Anytime something may happens may result in a state change, we send an action to the ngrx store

Actions are very simple in nature, an interface with a single string property `type1` is enough to describe an Action.
- any plain object with the `type` property can count as an action
- any additional props can be added to give more context to an event

```ts
// a way to dispatch an action submitting an issue
const submitAction = {
	type: "[Issue] Submit",
	issue: {
		id: randomID(),
		// other Issue props
	}
};

this.store.dispatch(submitAction);
```

> [!Note] Action Names
> ngrx doesnt care about names, as long as they are unique per type of action.
> This is mainly a readability feature during development and is particularly useful when use in tandem with the devtool.
> > worth thinking about, should avoid being too generic

## 8.1 Action Creators
An easier way of creating an action is to use the creator function `createAction()`  from `ngrx/store`

```ts
import { createAction, props } from '@ngrx/store';
import { Issue } from 'src/app/models/issue';

export const submitAction = createAction(
  '[Issue] Submit',
  props<{issue: Issue}>()
);
```

The generic type passed in to `props()` define any custom props (payload or metadata).
Notice how `createAction()` and `props()` make use of TS to enable sussinct code.

> confusing note below. does it mean unique name #review

Its important to not re-use (created) actions even if it does not contaim a payload.
So every action is a unique object and NgRx can work with those simple equality checks (shown in [[NilsNgRx - 7 - State]]).
So when an even occurs, you'll want to create and dispatch a new action to represent this specific event.

similar to states [[NilsNgRx - 7 - State#7.2 What not to put in the state|what to not put in the state]]
Only Plain/serializable objects should be added to the payload, this is to actions can be persisted and does not cause ==unwanted side-effects==

> Next containing notes on the code created for the action

> This goes through form, so there may be things I dont understand yet #review 
> https://angular.io/guide/reactive-forms

using `FormsModule` to reacte a reactive form with 2 controls for an issue text and priority.
Remember to import `ReactiveFormsModule` into application module.
For the forms, provide a `submit()` method to dispatch a sumbission payload while passing form value.

You could also create actions with additional logic by passing a function, this allow prep-processing of the payload.
Effectively we can outsource the ID generation instead of having this logic inside the component.

## 8.2 Action Hygiene

> generaly this covers the creation of action / action nameing
> might worth a #review pg45 https://www.youtube.com/watch?v=JmnsEvoy-gY

---

next chapter [[NilsNgRx - 9 - Reducers]]