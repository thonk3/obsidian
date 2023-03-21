# Bootstrapping

- Every app has a main entry point
- This app was built using the AngularCLI (built based on `webpack`)
This is ran by
```shell
ng serve
```

ng will then look at `angular.json` to find the entry point of the app
> Higher level explantion
- `angular.json` specifies a `main` file, here it is `main.ts`
- `main.ts` beint the entrypoint, will bootstrap our application
- the bootstrap process boots an ==Angular module== (explored later soon)
- we use `AppModule` to bootstrap the app
	- specified in `src/app/app.module.ts`
 - `AppModule` specifies which component to use as the ==top level== component
	 - in here its `AppComponent`
- `AppComponent` has `<app-user-list>` tags in the template and this renders our list of users.

For now lets focus on the Angular module system `NgModule`
 
Ang has a powerful concept of ==modules==.
When you boot an Ang app, youre not booting the component directly, but instead you ==create an NgModule== which points to the component you want to load.

```ts
// example NgModule
@NgModule({
	declaration: [
		AppComponent,
		HelloWorldComponent
		UserItemComponent
	],
	imports: [BrowserModule],
	providers: [],
	bootstrap: [AppComponent]
})
export class AppModule {}
```

Notice the `@NgModule` decorator 
Again ==decorators adds metadaata to the following class==

> We will loom more at `declarations`, `imports`, `providers`, `bootstrap`

## `declarations`
specifies the components ==defined in this module==
> components needs to be declared in `NgModule` before you can use them in your templates

think of it as its declaring a list of packages that are owned by this module

## `imports`
describe which ==dependencies== this module has.
were creating a browser app so imports `BrowserModule`

## `providers`
used for [[dependency injection]]
So to make  aservice available to be injected throughout our application, We will add here
> We will get learn more about this in [[ng-book 2 dependency injection]]

## `bootstrap`
 Tells angylar when this module is used to bootstrap an app
 we need to load `AppComponent` as the top level component


