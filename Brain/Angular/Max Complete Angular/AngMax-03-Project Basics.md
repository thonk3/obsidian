Recipe book / shopping list app

## Planning the App
> It is always vital to plan out what you are doing and structure out your app in a high level

Here we layout the structure / component heirachy

> - `Component`
> - feature

`Root`
- `Header` - navigation
- Shopping List
	- `Shopping List` - list display
	- `Shopping List Edit` - edit / input field / delete
- Recipe Book
	- `RecipeList`
	- `RecipeItem`
	- `RecipeDetail`
Model - data format / interfaces
- `Ingredient` 
- `Recipe`

---

## Creating the App

for now, dont create the `Ang` app in strict mode
```sh
ng new --no-strict <app-name>
```
install bootstrap css
```sh
npm i --save bootstrap@3
```
remember to add in the styles array

### Creating Components
Lets try creating the `HeaderComponent` manually, remember the parts to a component
- separate folder
- component file
- template file
- adding the component to `app.module.ts`

#### Creating Components via CLI
recipes feature
```sh
ng g c recipes
ng g c recipes/recipe-list
ng g c recipes/recipe-list/recipe-item
ng g c recipes/recipe-detail
```
shopping feature
```
ng g c shopping-list
ng g c shopping-list/shopping-list-edit
```

---
## Navigation Bar

Set up Header nav `template html`

---
## Recipes
### Creating `Recipes` MODEL

- Creating a class model
- can just effectively use vanilla ts to define the model

### Adding content to RecipesComponent
- now after finishing the model, we are using it in `RecipeList`
- render the list via `ngFor`

### Displaying Recipe Details

> So far its just html templates layout changes
> - I need to try to follow what the app is trying to do
> - what concepts the lessons are trying to teach

## Shopping List Component

> More templates set up I presume

up next [[AngMax-04-Debugging]]