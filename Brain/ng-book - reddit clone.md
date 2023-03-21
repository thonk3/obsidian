# App Information
![[ng-book - reddit clone info]]

# Getting started
Create new project from scratch
```shell
ng new angular-hello-world
```
for now use default css

![[Running Angular Locally]]

## App Root `src/index.html`
notice this part of the html
```html
<body>
	<app-root></app-root>
</body>
```
- this is where the application is rendered
- `app-root` is a component defined by the angular application
- in ng we can define our own html tags and provide custom logic to it
- right here `app-root` act as the ==entry point== for the application on the page

# Components
One of the core functionality behind Angular is ==Components==
- In `Ang` we write html markup that become our dynamic interactive apps
- But the browser only have a limited set up markup tags to combine and use

> The fundamental idea behind component
> Teach the browser new tags which have custom functionalities

creating a component via cli
```shell
ng generate component hello-world
## or 
ng gc hello-world
```

> lets update this [[Angular Component]]

A basic component has two parts
1. `Component` decorator
2. `Component` definition class

## Creating Component `hello-world`
### Inside Component `.component.ts`
```ts
import { Component, OnInit } from '@angular/core';

@Component({
	selector: 'app-hello-world',
	templateUrl: './hello-world.component.html',
	styleUrls: ['./hello-world.component.css']
})
export class HelloWorldComponent implements OnInit {
	constructor() { }
	
	ngOnInit(): void {}
}
```

### Component Decorators
now pay attention to this section
```ts
@Component({
	selector: 'app-hello-world',
	templateUrl: './hello-world.component.html',
	styleUrls: ['./hello-world.component.css']
})
```
This is called a Decorator
```ts
@Component({/* */})
```
Decorators are ==metadata added to code==
- this is "decorating" `HelloWorld` class as a `Component`
with the above decorator, it is 
- setting the `selector` as `app-hello-world`
	- sets component to be used by applying the `<app-hello-world>` tag
- setting `templateUrl`, sets the path of the html code to generate when angular see your `selector` called in the template

### Component Template
Angular template can be defined 2 ways
- Inline html via `template`
- External html template file via `templateUrl`

### Component Styling
similar to templates, style sheet can be both applied to the component via
- inline styling with `style`
- external css file with `styleUrls`

Angular use a concept called [[Style Encapsulation]]
- the style for a specific component only apply to that component

> this will be explored more within [[Advanced component]]

### Using the component
now you can try using this component in `app.component.html`
by referencing to what is set as a selector as a DOM element

# Adding data to Component
OK so now the component is only rendering a ==static== template
Imagine an app that will show a list of users displaying their name
- Before rendering a whole list
Lets learn how to render an individual user

Lets create a new component then display it in the app, adding the template to `app.component.html`
```shell
ng g c user-item
```

## `UserItemComponent`
The purpose of this component is to display the name of a user

lets introduce the name as a `property` of or component, this way, the property can be used re-used to dynamically show different user's name

```ts
export class UserItemComponent implements OnInit {
	name : string;

	constructor() {
		this.name ="egg"
	}

	ngOnInit(): void {}
}
```
2 things was changed

### property
here we declare a name `property` and assigning its type to string

### constructor
`Constructor`s are functions that is called when we create a new instance of the class

### Rendering the template
```html
<p>Hello {{ name }}</p>
```
Notice the syntax `{{ name }}`
This is called template tags

The content inbetween the tag will be expanded as an expression

---
# Working with arrays
Now we are only printing a single name,
But what about a collection of name

using the syntax `*ngFor` in angular, we can iterate through a list of object
> The idea is to ==repeat== the same markup for a collection of objects

lets start with a new component `user-list`
and replace `user-item` with it inside the root app template

same with `name` prop for `user-item` lets add a property `names` for the collection of uesr names inside our new component `user-list`

now we can now use `*ngFor` in `user-list` template 
again, this will
- iterate over a list of items
- generate a new tag for each one

```html
<ul>
	<li *ngFor="let n of names">Hello {{ n }}</li>
</ul>
```

> In here we say:
> we use the `ngFor` directive on this attribute,
> similar to a `for` loop, creating a new DOM element for every item in collection

#beyond_learning
you can learn alot about how Ang team write its component by looking at the source code
e.g [ng for directive source code](https://github.com/angular/angular/blob/main/packages/common/src/directives/ng_for_of.ts)

## Using the UserItem component
Now we're changing `UserItem` to be used by `UserList` instead of rendering each name.
> instead of rendering the text directly,
> we let `UserItem` component handle the template/functionality of each item in the list

regarding changes 
1. change `UserList` to render `UserItem` in the template
2. change `UserItem` to accept the `name` variable as an `input`
3. change `UserList` to pass the name to `UserItem`

### Rendering `UserItem`
`src/user-list/user-list.components.html`
```html
<ul>
	<li *ngFor="let n of names">
		<app-user-item [name]="n"></app-user-item>
	</li>
</ul>
```

### Pass data to `UserName`
Now to accept data input from parent task, we can use the `@Input()` decorator, for now just know this let you pass a value from the parent template

To pass values to a component, we use the `[]` syntax in the template

> This is saying we want to assign `[name]` attribute in `app-user-item` component with the value from `n` 

Passing value into a property of the child component


---
# Next Section
[[ng-book 2 bootstrap crashcourse]]
continuing with the application
[[ng-book 2 expanding the reddit application]]

---
# Changelog
- 2023-01-28 - init 