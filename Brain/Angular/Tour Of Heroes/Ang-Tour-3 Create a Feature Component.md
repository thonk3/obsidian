So far everything is living within `HeroesComponent`
- displaying the list
- viewing the detail

For larger projects, this would be hard to maintain.

> This section splits up large components to smaller specified subcomponents.
> This will ends up with
> 1. `HeroDetailComponent` present the details of a selected hero
> 2. `HeroesComponent` presenting the list

## Make the component

use the cli to create a new component `hero-detail`
```
ng generate compoment hero-detail
```

this cretes the scafold containing the dir `src/app/hero-detail` where 4 files are created
- the css file
- the html file
- the ts component file `HeroDetailComponent`
- the test file for the component class
this also adds the `HeroDetailCompoentn` as declaration within `@NgModule` decorator in the mail `app.module.ts` file

### Write the template

now we cut the old detail from the `HeroComponent` and move it into the new `HeroDetailComponent`

### add the `@Input()` property

the `HeroDetailComponent` template binds to the component `hero : Hero` property

to use it, first import the type 
```js
import { Hero } from '../hero';
```

the `hero` prop must be an `Input` prop annotated with the `@Input()` decorator because the parent(external) component binds the prop to component like this
```js
<app-hero-detail [hero]="selectedHero"></app-hero-detail>
```

declare the prop with with the `@Input()` decorator like this
```
@Input() hero?: Hero;
```


## Show the component

The `HeroesComponent` used to display the hero details on its own, before the parts is removed in this template

> This part guides through delegating logic to the `HeroDetailComponent`

`HeroesComponent` and `HeroDetailComponent` have a parent/ child relationship
- parent `HeroesComponent` control the child by sending the selected 

### updating `HeroDetailComponent

now the Hero Detail component selector is 
```html
<app-hero-detail [hero]="selectedHero"></app-hero-detail>
```

This is one-way binding from `selectedHero` of the parent component to `[hero]` prop 

---

## Summary

- You created separate reusable `HeroDetailComponent`
- used property binding to give the parent `HeroesComponent` control over the child `HeroDetailComponent`
- use `@Input` decorator to make `hero` prop available for binding by the external `HeroesComponent`