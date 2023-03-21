
There is no set of pre-defined structure or a "best practice" that you strickly need to follow.
But having a clear structure / pattern to organizing your state models/reducers/actions can prevent your codebase from being messy.

The "best" structure is depending on your preference or what works well for you and your team. The important part is consistent.

Naming convention
- similar to component files 
- its recommend to have a separate file for every part of the store and apply the same pattern
- have the file ends with `.reducer.ts` / `.action.ts` / `selector.ts` / `effects.ts`

Anything related to the store goes into `store/` dir at the root level of the app.

Feature specific fules placed into corresponding sub-dirs.
Optionally creating a separate `index.ts` where all state slices comes together to define the root state of the application and how it is managed by individual reducers.
Keep configs out of your module declarations as much as possible.

A initial file structure you can follow:
```
src
|_app
	|_store
	|_index.ts
	|_issue
		|_issue.actions.ts
		|_issue.reducer.ts
		|_issue.state.ts
```

Try not to group type of code together (all reducers into a dir...)
Try to always group by feature to co-locate code that works together, its likel that this code also changes together.

> notes on import/ exports standards

The model for a state slice maybe defined in an interface inside the corresponding `.state.ts` file.
you may also wants to export an initial state that implements the Interface from there.

reducer files hould always export a single reducer function, preferrabbly prefixed with the state prop its ment for.

> Something about Ang's ivy engine

And then everything is wired together inside index.ts by defining a type for the root state and exporting a reducer mapping
```ts
/* index.ts */
import { ActionReducerMap } from '@ngrx/store';
import { issueReducer } from './issue.reducer';
import { IssueState } from './issue.state';

export interface RootState {
	issue: IssueState;
}

export const reducers: ActionReduceMap<RootState> = {
	issue: issueReducer,
}
```

Lastly, register the reducer mapping through `StoreModle.forRoot()` in the app-module. we can then inject the store by providing

> alot of information which i need to review after gaining more understanding

---

next chapter [[NilsNgRx - 7 - State]]