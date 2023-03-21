> [!Note] main source
> https://ngrx.io/guide/store/actions

One of the main Building blocks of NgRx. The role of actions are:
- express unique events that happen through out your application.
- the IO of many systems in NgRx. 
- help you to understand how events are handled in your application.

## Actions Interface
an action in `ngrx` is made up of a simple interface
```ts
interface Action {
	type: string;
}
```
it has a single property `type` represented as a string.
the property is for describing the action that will be dispatched in your application usually with the format of `[source] event`.
Its best use to provide the context of the action and where its dispatched from.

Props can be added into actions to provide additional context or metadata for an action.

Here are some actions examples written in plain JSObjects
```js
{
  type: '[Auth API] Login Success'
}
```
plain action describing event triggered by a successfull auth after interacting with backend API
```js
{
  type: '[Login Page] Login',
  username: string;
  password: string;
}
```
action describes the login event in the login page attempting to authenticate a user.
`username` and `password` are defined as additional metadata provided from the login page

## Writing Actions

Some rules on ==writing good actions== in your application
- **Upfront** - write actions before developing features to understand and gain shared knowledge of implemented feature
- **Divide** - categorize actions based on event source
- **Many** - actions are inexpensive to write, the more actions are written, the better  you can express flows in your application
- **Event-Driven** - capture events **not** commands as you are separating the description of an event and the handling of that event
- **Descriptive** - provide context that are targetted to aunique event with more detailed info, which can be use to aid in debugging

lets look at an example action of initiating a login request.
```ts
// login-page.actions.ts
import { createAction, props } from '@ngrx/store';

export const login = createAction(
	'[LoginPage] login',
	props<{ username: string, password: string}>()
);
```
`createAction()` returns a function, thats when called, return an object in the shape of the [[NgRx Actions#Actions Interface|Action Interface]]
the `props<>()` method is used to define additional metadata needed for handling actions.
Action creator provide a consistent, type-safe way to construct an action.

use action creator to return `Action` when dispatching
```ts
// login-page.components.ts
onSubmit(u: string, p: string) {
	store.dispatch(login({username: u, password: p}));
}
```

the `login` action creator recieves an this action object
```ts
{
	type: '[LoginPage] login',
  {
	  username: u,
	  password: p
  }
}
```

The returned action has a very specific context about where the action came from and what event happened
- the category of an action is captured within the `[squared bracket]`
- the category is used to group actions for a particular area
- the `Login` text after category is a description about what event occurred from this action

> [!Note] Class base actions
> can also be written, this is the previously defined way to create actions before actions creators are introduced.
> [more on classbase actions for v7.x and prior](https://v7.ngrx.io/guide/store/actions)


---
## Next steps
Action's only responsibilities are to express unique events.
Learn how they are handled in the other building blocks of NgRx

- [[NgRx Reducers]]
- [[NgRx Selectors]]
- [[NgRx Effects]]