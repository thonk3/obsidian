
## Overview

- Attributes Directives
	- sits on elements/attributes
	- Only change elements theyre attatched to 
- Structural Directive
	- change DOM behaviour
	- what `*` means

---

## Recap

### ngFor
review for loops

### ngIf
review if condition

### ngClass
review ngClass attatching styling class on condition

### ngStyle
conditional inline styling

---

## Creating Attribute directives

> [!info] code in `basic-highlight`

```ts
//vscode directive snippet
import { Directive } from '@angular/core';

@Directive({ selector: '[selector-name]' })
export class NameDirective {
  constructor() { }
}
```

The important part of the directive is the selector - to tell angular how this is is used in templates

use the constructor to injects the element, where the directive sits on 
```ts
constructor(private elRef: ElementRef) {}

ngOnInit():void {
	this.elRef.element.style.backgroundColor='green';
}
```

> [!note] `private` keyword
> prop short hand allowing it to be accessed within the class scope

To use this we need to
- Like components, declare the directive within `app.module`
- use it within the template
```html
<p appBasicHighlight>Style me with basic directive!</p>
```
  
### Building a Better Attribute Directive

The last section, accessing elements directly via DI is not best practice
A better way to use directives is through the `Renderer2`

> [!info] code in `better-highlight`

```shell
ng g d better-highlight
```

> [!Note] `ngOnInit` vs `constructor() ` 
> [read later](https://stackoverflow.com/questions/35763730/difference-between-constructor-and-ngoninit)
> #beyond_learning 

> [!Note] Not sure why this is better 
> [more on `Renderer2`](https://angular.io/api/core/Renderer2)
> #beyond_learning 
> 

---

## Host Events
using `HostEvents` to listen to host emitted events

```ts
  @HostListener('mouseenter') mouseOver(eventData: Event) {
    this.elementRef.nativeElement.style.backgroundColor = 'green';
  }
```

## Host Bindings
using `HostBinding` to interact with host element's properties
```ts
@HostBinding('style.backgroundColor') backgroundColor: string = 'pink';
```

## Binding to Directive Properties
In other words passing data into directives
This is done via custom property binding
```ts
  @Input() defaultCol = 'transparent';
  @Input() highlightCol = 'pink';
```
```html
<p 
	 appBasicHighlight 
	 [highlightCol]="'red'" 
	 [defaultCol]="'yellow'">
	 Style me with basic directive!
</p>

<!-- this overrides the setting in the bound directive -->
```

if an alias is set for a `Input` prop you can bind the value like this
```ts
 @Input('appBasicHighlight') highlightCol = 'pink';
```
```html
<p 
	 [appBasicHighlight]="'yellow'">
	 Style me with basic directive!
</p>

<!-- this overrides the setting in the bound directive -->
```

## Structural directive
explaining the `*` 
Angular transform thesse directives to something else

#not_important https://www.udemy.com/course/the-complete-guide-to-angular-2/learn/lecture/6656182#notes

#skip https://www.udemy.com/course/the-complete-guide-to-angular-2/learn/lecture/6656186#notes


## ngSwitch

