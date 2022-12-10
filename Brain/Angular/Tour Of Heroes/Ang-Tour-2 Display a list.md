This tutorial shows:
- expand the application to display list of heroes
- allow users to select hero and display the details

## Displaying heroes

with the list of heroes,
the list can be displayed with `*ngFor` in the template

> this itterates through your array and render the html list

on interactive elements:
- using html that are inherently interactive instead of listerners accessability interactability
- more deaills on [accessability in angular](https://angular.io/guide/accessibility)

> skipping styling because ofcourse

---

## Viewin details

next part is letting the user view all details of the hero when selected

### Add click event binding

now we adding event.
[event binding syntax](https://angular.io/guide/event-binding)

The round bracket around `click` tells ang to listen for the `<button>` on click event to trigger the bound function

Next section we define the `onSelect()` method in `HeroesComponent` to display the selected hero from `*ngFor`

### Add detail section

now add a section in the `heroes.component.html` and have it rendered conditionally only if theres a hero selected

### Style selected hero

the css here is essentially the same.

This part introducing Angular's [class binding](https://angular.io/guide/class-binding) to 
add/remove classess conditionally to the element you want to style

`[class.css-class]="condition"`

---

## Summary

- learn how to display a list using `*ngFor`
- learn how to conditionally render html with `*ngIf`
- toggle css style with `class` binding


