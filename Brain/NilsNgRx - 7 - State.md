
All because of TS, we're able to declare ==static type==
This should be used everywhere and anywhere that is dealing with the state.

in TS you can define data models with either using interface or type declarations
e.g to define the shape of a single issue with an interface
```ts
export interface Issue {
	id:string;
	title: string;
	description: string;
	priority: "low" | "medium" | "high";
	resolved: boolean;
}
```
or using the `type keyword
```ts
export type Issue { /* */ }
```

[Type alias declaration](https://www.typescriptlang.org/docs/handbook/advanced-types.html#type-aliases)
are generally more powerful since they can give a name to any type??
Including things like functions or primitives.

> This is also a preference
> The Auth tend to use interfaces in most cases and some type aliases for tuples or union

Again, the base shape should be oulined by an interface inside `<feature>.state.ts`.
How ever you can also incorporate models from other locations as long as they meet some conditon (`see 7.2`)

lets start with the first draft of the application state, 
containing a list of entities and current active search filter.
and an initial state for this type containing an empty list and empty search text.

> [!Note] A good idea
> is to populate the initial state with defensive and valid values

If you decide to set property to `undefined` make sure the consumer can deal with that.
Again it is up to you and the application.
It is also possible to retrieve state from `localStorage` (see `Re-hydration 16.3`)

## 7.1 Normalization
Models with unique identifier are best stored in an object where the identifier is used as a key while the model instance represents the corresponding value.
We can specify such a setup as an interface with an index type
```ts
// issue.state.ts
export interface Issues {
	[id: string]: Issue;
}
```
This says taht object of type `Issues` is a dictionary having the string ans a key and `Issue` as object value.
The type can then be used as a replacement for the list
```ts
export interface IssueState {
	entities: Issues;
	filter: Filter;
}
```
The corresponding initial state should change to an empty dictionary object

When accessing a specific issue, we can now just use the bracket notation with an ID
```ts
const specificIsue = entities[id];
```

the dictionary can be de-normalized into a list to be iterated with `*ngFor*` by using `Object.values()` / `Object.keys()` / `Object.entries()`

Such normalization are usually performed by selectors wich will be explored later on.

In other ways,
==state normalization== also refer to having the same data item only in a single place. 
e.g. implementing a multi-selector for the list of isses. In order to know which ones are selected, we might be tempted to manage another dictionary in the store.
```ts
export interface IssueState {
	entities: Issues;
	selected: Issues;
	filter: Filter;
}
```

OK so, in the case of when one issue is updated, we need to make changes both inside `entities` and `selected`.
Since the state in immutable and we can only create new objects with reducers, changing one ditionary will not affect the other.
This state can actually be simplified, all it needs is to keep track of which issues were selected, simply a list of reference of the selected issues inside the `entities` property
```ts
export interface IssueState {
	entities: Issues;
	selected: string[];
	filter: Filter;
}
```

## 7.2 What not to put in the state
There are many things that does not beling in NgRx store - some for conceptual reasons, some for technical reasons

### Derived State
- anything computable from existing state does not need to be in the state
- even if the computation is expensive
- we can write selectors for this purpose, to recompute data when necessary.
- If derived state is put in the store, we will have to also manage the same information in multiple places, increasing chances of making mistake

### Local State
This is relatively difficult to gague
- it is hard to know on which level state should reside now/in the future
- some example are obvious - should not keeptrack if a dropdown is open or closed
- while you may need the log in status in many places, that is something for the store

Some times cases it is hard to determine
e.g. reactive forms
- they track their own state and often it is good enough to only put submitted value into the store
- BUT some use case may benefit from syncing forms with NgRx to retain their values between navigations and allowing for easier debugging.

> [!Note] rule of thumb
> If some state is only relevent to one component, manage it locally.
> You can always start with local state and lift it up to the store later when necessary

> words of other solution for managing local state

### Classes and Special Objects

Developers with a background in OOP naturally will gravitate towards classes in TS.
Angular too makes heavy uses of them but it ==doesn not really fit with NgRx== 
Classess are commonly used in a mutable fashion where we cahnge the inner state by calling instance methods.

> NgRx embraces immutability.

Reducers are supposed to compute a ==new state without modifying the last one==.
This rule is broken if we work with mutable calsses and re-use them for later states.

this can create problems like
- harder to ypdate the view when state changes as NgRx relies upon simple reference checks for that.

With plain objects, where we can alway create a new state instead of modifying the latest one.

> very cool demo on creating a new state,
> essentially the newstate object reference is compared with the previous state ref to detect a change.

Another pain point `serialization`.
Transform a class instance to JSON with `JSON.stringify` might work.
But parsing the result with `JSON.parse()` will just give you a plain object.
Your js `prototype` chain is ==not recovered==.
This makes many use-case more difficult (debugging / re-hydrating)

> Things regarding `map` or `set` I do not understand yet
> #review

Despite classes you should avoid some of the following objects in your state as this can hinder garbage collection and lead to hard to debug errors:
- functions
- blobs
- dates (try `Date.toJson()` or similar)
- promises
- obserbables
- html elements
- `window` and similar

> its best storing only plain, serializable objects in the state while still using interface or type aliases for type safety


---
next chapter [[NilsNgRx - 8 - Actions]]







