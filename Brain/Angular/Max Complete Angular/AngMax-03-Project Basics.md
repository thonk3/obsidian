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

#todo vid part 49 end