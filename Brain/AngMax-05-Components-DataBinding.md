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
regarding css encapsulation
- by default, css does not care for encapsulation, style applies to all matching tag/class/id
- this default behaviour is disabled by Angular, a component css will only apply to that component template

but it is possible to overwrite this behaviour via the decorator of the component
> #review72 for more info regarding css bugs

## Local References

#skip73


## Component lifecycles

---
## Summary



---