Understanding Components and DataBinding

> Workthrough using the example project provided

## Simplifying project into components
- Again it is never ideal to have all business logic and ui template bundled uptogether in a single component

now we are splitting this example app into
- Cockpit
- ServerElement

> Essentially this sets up to show how to
> - pass a common property from parent to many child elemets 

## Property & Event Binding
> Overview seems pretty important #review
- The purpose of binding is to bind value into DOM elements
	- Passing data into a html element
- Same with event binding
	- the button emit an event we are able to listen
 
> properties and events both have built in and custom instances

### Binding to custom properties
When using custom properties
- by default, all props of components are only accessible by that component
- To allow the parent component to access the prop, the `@Input()` decorator must be called
```html
<app-child-component [item]='dataFromParent'></app-child-component>
```
```js
export class ChildComponent {
	@Input() item;
}
```
you can also assign an alias to the property by passing an arg to the `Input` decorator
```html
<app-child-component [srvItem]='dataFromParent'></app-child-component>
```
```js
export class ChildComponent {
	@Input('srvItem') item;
}
```

### Binding to Custom events
Now we're demonstrating how to pass something from the child component to the parent component

> what if something changes in a component, and we want to notify the parent of that change

#### Creating an Event emitter

#### Listening to custom event

### Custom Property and Event Binding Summary
What we learn thus far `Component Communication`

what `@Input()` can do

what `@Output()` can do

use cases

often used to change dynamic interaction of data within different components
- chain can get complex very fast
- not very ideal when communicating data across many level of component
> different method will be shown to better achieve such ability

---
## View Encapsulation
This section talks about inheritance heirachy of css styles between components

regarding css encapsulation
- by default, css does not care for encapsulation, style applies to all matching tag/class/id
- this default behaviour is disabled by Angular, a component css will only apply to that component template

but it is possible to overwrite this behaviour via the decorator of the component `@Component`
> #review -Part72- for more info regarding css bugs
> This part is lightly go through because it 

## Local References

This is another way of geting data values from a child component without using two-way binding
- Since we only want to use the input data at the point of button click
- its good enough to only get that value at a singular point of time
This is done via references `#referenceName`

Its important to note that references are only accessible **ONLY** within the templete they are created
> You cannot use this reference in your ts component logic

```html
  <label>Server Name</label>
  <input type="text" class="form-control" #serverNameInput>
  <label>Server Content</label>
  <input type="text" class="form-control" #serverContentInput>

  <button
	  class="btn btn-primary"
    (click)="onAddServer(serverNameInput, serverContentInput)">
    Add Server</button>
```
```ts
function onAddServer(sName: HTMLInputElement, sContent: HTMLInputElement) {
	console.log(sName.value, sContent.value);
}
```

## Access to Template & DOM via `@ViewChild`
This is another way of accessing local references or any element within our app via the `@viewChild` Decorator

> This is just to show you this tool exist
> Not best practice

### Versioning Note on `@ViewChild`

In **Angular 8+**, the `@ViewChild()` syntax which you'll see in the next lecture needs to be changed slightly:

Instead of:
```ts
@ViewChild('serverContentInput') serverContentInput: ElementRef;
```
use
```ts
@ViewChild('serverContentInput', {static: true}) serverContentInput: ElementRef;
```

The same change (add `{ static: true }` as a second argument) needs to be applied to ALL usages of `@ViewChild()` (and also `@ContentChild()` which you'll learn about later) IF you plan on accessing the selected element inside of `ngOnInit()`.

If you DON'T access the selected element in `ngOnInit` (but anywhere else in your component), set `static: false` instead!

If you're using Angular 9+, you only need to add `{ static: true }` (if needed) but not `{ static: false }`.

## Projecting content into Components with `ng-content`

This is essentially `{props.children}` in react

## Access to Template & DOM via `@ContentChild`

#skip
> This part is skipped as well because its not good practice
> Shouldnt mess to much with the dom manually

## Component lifecycles
> In other words React lifecycle functions

Common lifecycles
- `ngOnChanges` - called uppon a bound input prop change, prop with `@Input`
- `ngOnInit` - called once the component is initialize / runs after constructor
- `ngDoCheck` - called during every change detection run
	- Seems like a closer look at docs is needed
	- this seems like the depenency array of `useEffect`???
 - `ngAfterContentInit` - called after content (`ng-content`) has projected into view
 - `ngAfterContentInit`
 - `ngAfterViewInit`
 - `ngAfterViewChecked`
 - `ngOnDestroy` - called before the component is about to be destroyed

> Hooks are pretty cool, and useful in general 100% deserve a #review

### Lifecycle Hooks in action

This logs things out and demo how and when each Lifecycle functions are called
> Good Practice:
> for each lifecycle hook you decide to call in your component
> make sure the component implement its interface 


---
## Practice - Property/Event bindings & View Encapsulation

1. Create 3 component - GameControl, odd even
2. GameControl should have buttons to start and stop the game
3. On game start
	- Event (holding increment number) should get emitted each second (`ref = setInterval()`)
4. Event should be listenable from outside component
5. When stopping the game, no more event should get emitted `clearInterval(ref)`
7. Simply output `Odd - NUMBER` or `Even - NUMBER` in the two components
8. Style the element holding our output text differently in both component

### Component Heirachy
Root
- Control
- Even
- Odd

### My solutions
> Heirachy is the same

In root
- kept the current number as its own value
- the number is passed into `Even` `Odd` to display
- kept 2 functions to either start the counter and end the counter
- these functions are then passed into `Control` to catch the emit event
Control
- 2 custom even emitter bind to button on click
Even/Odd
- read passed in `number` prop and display as applicable 

### Max Solution
> Heirachy is the same

differences with my solution

as the name describes it the `Control` component handles all business logic of the app

`Control` component 
The start game button triggers an `interval` loop that emits an event object containing the counter

The root component would then triggers an action that handles the emitted object

---

Up next [[AngMax-06-Project Component & DataBinding]]