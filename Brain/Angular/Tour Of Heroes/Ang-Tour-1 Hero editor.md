
next step is to create a new component to display hero information and place that in the application shell

## Creating heroes component

use the ang cli to create the new component `heroes`
```shell
ng generate component heroes
```   

it creates the new component dir `src/app/heroes` and generate 3 files of the `HeroesComponent` along with the test file

In the class files
- you always import `Component` symbol from the ang core library 
- `@Component` is a decorator function that specifies the angular metadata for the component

`ng generates` create 3 metadata props
- `selector` components css element selector
- `templateURL` location of the components template file
- `styleUrls` location of the component's private css styles

the `ngOnInit()` is a [lifestyle hook](https://angular.io/guide/lifecycle-hooks#oninit)
its called by ang shortly after creating a component, good to put initialization logic

> Always export the component class so you can import it else where

Add hero property to the `HeroesComponent`
and show the `HeroesComponent` view in the main App Component

--- 

## Adding interface 

Now we're adding an interface to set up the Hero object.
After this you need to update the template file to display the new object data

---

## Pipe formatting

you can format data with a pipe like

```html
<h2>{{ hero.name | uppercase }}</h2>
```

the word `uppercase` in the interpolation binding after `|` activates the built in `UppercasePipe`

[Pipes](https://angular.io/guide/pipes) are a good way to format strings, currency amounts, dates and other display data. Angular ships with several built-in pipes and you can create your own.

---

## Edit the hero

Users should be able to edit the data via `<input>` text box.
It shouuld both display the `name` property and **update** that property as the user types.
That means data flows from the component class out to the screen and from the screen back to the class

Now we set up the **two-way** binding between the `<input>` element and the `hero.name` property

## Two-way binding 

first we refactor the `HeroComponent` template to
```html
<div>
  <label for="name">Hero name: </label>
  <input id="name" [(ngModel)]="hero.name" placeholder="name">
</div>
```

the `[(ngModel)]` is angular's two way binding syntax.
It binds teh `hero.name` prop to the to the HTML text box so that data can flow in both directions.
Data can flow from `hero.name` prop to the text box and from the text box back to `hero.name`

## Missing [FormsModule](https://angular.io/api/forms/FormsModule)

OK so after updating the template, the app stopped working when you add `[(ngModel)]`

This is because as `ngModel` is a angular directive from `FormsModule`, its not available by default.

---

## AppModule

Angular needs to know how pieces of your application fit together, and what other files and libraries the application requires.
This is called metadata

teh `@NgModule` decorator annotates teh top-level `AppModule` class containing critical meta data
And this is where you opt in to the `FormsModule`

Add the `FormsModule` to the `imports` array in `@NgModule`.
This array contains the list of external modules that the application needs.

---

# Summary

- used `ng generate` to create new components
- displayed the new component
- applied format piping
- use two-way data binding with `ngModel` directive
- `AppModule` overview (imports, declaring components)