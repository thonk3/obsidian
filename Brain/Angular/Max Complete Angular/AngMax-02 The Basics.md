> Info I already know but is important
> [How the angular App is Loaded and Started](https://www.udemy.com/course/the-complete-guide-to-angular-2/learn/lecture/6655700)

> This lesson is followed through with the git project [01_basics]()

`@NgModule` decorator metadata
- `bootstrap` array - list components that should be known to Ang at the point of reading Index html
- `declaration` array - list of registered components for ang to recognizes

## Angular Components
- `AppComponent` main root component

hes making a `app/server` component manually instead of the CLI
- `ng generate component server` would be ok
- `server.component.ts` exporting the `ServerComponent` class
	- `@Component` [[TS Declarator]]
		- `metadata` explanation
			- `selector` - html tag to refer the class
			- `templateUrl` - dir to the html template
	- [[TS Declarator]] are a TS feature that 'Enhances' your classess and more

### The Role of AppModule with component declaration

AppModule
- Angular uses components as building blocks of your place
- Uses Modules to bundle different pieces of your app
- For new components
	- Needs to be registered in the AppModule to angular to recognize its existance
	- Under `@NgModule` metadata
		- `declaration` add the new class component that was just created

### Components via the CLI
```bash
ng generate component <component>
## or
ng g c <component>
```
### Components Templates and Styling
- Can use Inline styling
- Can Use Inline HTML within the `@Component` declarator and in the `template` metadata string
- Plain Css styling is pretty basic

### Component Selectors
Regarding the `@Component` declarator, the `selector` metadata, there are many things you can do with it
- Use to mark the `html` tag reference by passsing a regular string
- Used to mark the selector as an `attribute` by encapsulating the string like `[app-selector]`
- Used to mark the selector as a `class` by prepend the string with a dot `.app-selector`

> Not sure when the different selectors are used, hence this is still trivial info

## Practice Components

Basic Practice on creating components
1. Create new Components `WarningAlert` and `SuccessAlert`
2. Output beneath eahh other in `AppComponent`
3. Output a warning or sucess message
4. Styling (optional)

### Components Solution
- Create components via CLI
- Output in AppComponent template
- Output message via string

---

## Understanding Data Binding

> Brief knowledge

- Databinding == Communication
- Communication between your TS Code (Logic) with the Template

Different ways of DataBinding
- Output data (One way Binding)
	- String Interpolation `{{ data }}`
	- Property Binding `[property]='data'`
- React to (User) Events (one way)
	- Event Binding `(event)='expression'`
- Combination of both (Two way  binding)
	- `[(ngModel)]="data"`

### String Interpolation
string interpolation conditions
- Can use terinary expression
- Any expression resolved to a string is ok
- Cannot use blocks (if / esle)
- Cannot use multiline expressions

### Property Binding
Property binding allow you to dynamically bind a property to

> Consider situations where its best to use `string interpolation` vs `property binding`


`[]` indicates propery binding
- dynamically bind a value to a property in DOM\

This example binds a boolean value to the `disabled` property of the DOM
```html
<button
	[disabled]="!disableFlag"> Add </button>
```

### Events  Binding

> Walk through how to add a button to create a new server

`()` indicates event binding
- built in with angular, can bind to all events relating to the html tag

This examples binds a function call into a button `onClick` event attribute
```html
<button
	[disabled]="!disableFlag"
	(click)="clickFunction()"> Add </button>
```

### Bindable props and events

- To find out which props or events of `html` elements you can use
- good idea is to `console.log` out the element too see what props/events it offers
- or look up documentation

### Passing and Using Data with Event Binding

`$event` data emited by the event
- using in tandem with `(input)` triggers every keydown
- reserved keyword which gave us access to the event data

This examples bind a function call to the `on input change` event for the `input` elements.
Which uses the `$event` binding to pass the emited event object to the function
```html
<input
  type="text"
  (input)="onUpdateServerName($event)"/>
```

### Two-way data binding

> NOTE:
> `FormsModule` is required for two-way binding
> - need to enable `ngModel` directive, by adding `FormsModule` to the `imports[]` array
> - `FormsModule` is imported form `@angular/Forms`

- combination of property and event binding
- syntax `[()]` using the `ngModle` directive

### Combining many forms of Data Binding
> Walk through, enable the "add" button to add a new server item

### Practice binding

1. add input field which updates `username` prop every keystroke using `two way binding`
2. output username property via `string interpolation`
3. add `button` whis is only clickable if `username` is not empty string
4. `onClick` - reset the `username to empty string`

> work done in `01_basics/practicing-components2`
> NOTE:
> - over engineered with input calling a checker function
> - simpler method is to bind the boolean to check `username` within the `[disabled]` prop in `button`

---

## Directives

- Directives are instructions in the DOM
- `Components` are a kind of instructions in the DOM
	- they instruct Ang to add the content/logic in to places via the `selector`
Examples directives
```html
<p appTurnGreen>wasd</p>
```
```js
@Directive({
	selector: '[appTurnGreen]'
})
export class TurnGreenDirective{}
```

### Conditional rendering
> Introducing to the `ngIf` directive
> to only display the server added string after the button is clicked

`ngIf` is a structural directive using to conditionally render something, it takes in a boolean value
```html
<p *ngIf="isCreated">Created server {{serverName}}</p>
```
introducing to `#` marker / local reference
introducing to `<ng-template` can use to mark places in the DOM

`<ng-template #noServer` is a component marking a local reference in the [[Document Object Model]] we want to show conditionally
Which is trigger by the else condition within `*ngIf`
```html
<p 
	 *ngIf="serverCreated; else noServer">
		 Created server {{serverName}}
 </p>

<ng-template #noServer>
  <p>No Server created</p>
</ng-template>
```

> `else condition seems pretty weird`

### Considiontal styling `ngStyle`
we are now conditionally adding inline css via `[ngStyle]` (prop binding directive)
- `ngStyle` itself is a `directive` and not related to property binding `[]`
- adding the property binding syntax `[]` tells Ang we wants to bind some data into the directive `ngStyle`
- the property takes a `js object`  where you provide the css object

#### Applying css Classes `ngClass`
while `ngStyle` allow you to dynamically add style
`ngClass` allows you to dynamically change classes

`[ngClass]` directive takes in json containing key value pairs where
- `key` the class
- `value` the condition

### Outputting Lists
`*ngFor` directive itterate through array and render list
```js
<li *ngFor='let i of Items'/>
```

> currently we can add items into the server array
> but have not learn how to pass serverName into the `app-server`
>
> this will be explored soon in later section
> - how to create our own props component which can be set outside of that component

### Practice Directives
1. add button to `display details`
2. add p with any content
3. toggle displaying of that paragraph with the button
4. Log all button click into an array below (timestamp or an increment number)
5. from 5th item, give all log items a blue bg via `ngStyle` and white text `ngClass`

> work done in `01_basics/practicing-components3`
> everything is the same, they used a number array instead of index

### `ngFor` index
Getting array index out of `ngFor` itteration directive

```html\
<p *ngFor='let ii of items; let i = index'/>
```

---

## Section 2 Summary


Up next [[AngMax-03-Project Basics]]