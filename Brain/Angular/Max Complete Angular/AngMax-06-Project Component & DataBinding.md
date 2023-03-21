> Now going back to the Recipe/Ingredients Project to apply what we learned

## Adding navigation with Event Binding

Now we-re adding access to either the `Recipe` or `ShoppingList` component using `ngIf`
- Lets try it myself first then go through with max later

> Now this is not the ideal way to do `navigation` but to practice what we learn so far
> A more Ideal way to handle `navigation` will be shown later on

### My nav implementation

In the `root app` component
- listens to a custom event `onNavChange` (nav Output) which triggers `onNavEmitted` which set the active view
- each view component is conditionally rendered via `activeView` object
In the `nav` component
- each nav element contains a different `OnClick` function
- when click they both trigger the same `onNavChange` event emitter
- emitting different view objects

> Max Recipe project walkthrough seems intersting
> Its determining what to display via a string 
> - an improvement to this would be an enum for 

## Passing Recipe Data with Prop binding
Now we working on Recipe list,
now implementing recipe-item then loop through the recipe array to display the list

> Straight forwad, pass an object from and array to an item list

## Passing Data with event/prop binding
Now implement - on Recipe Item click,
the item will emits something that will populate the recipe detail section with the selected recipe

> Feels a bit weird in my attempt to emit 2 event twice to pass data back through 2 levels of components

> OK difference with his method is
> he also does double emit action
> - one from recipe-item that trigger on select
> - one from recipe list to pass object to parent
> The difference is he does not emit a recipe object in the recipe-item
> The object is retrieved from `ngFor` loop in the list and is passed via function args of another emitter in `List`

## Allow User operations
Moving to Shopping list, allowing the user to add now shopping list item via the edit form

> USING REFERENCE WHY
> first we practice with normal binding then try reference

standard emit object on button click

> Reference try `ViewChild` `ContentChild`

Ah simple - pass the local reference as parameter as argument

> try `ViewChild` like max

---

Up next [[AngMax-07-Directives]]