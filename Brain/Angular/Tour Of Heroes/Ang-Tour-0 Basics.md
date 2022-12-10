# Angular tour of heroes

The tour will show an introduction to fundamentals of angular
- Set up local angular dev environment
- use angular CLI for application

the rest of the design can be seen on the [tutorials page](https://angular.io/tutorial)

---

# Creating a new project

This tutorial be teaching to
1. sets up your environment
2. creates a new workspace and initial application project
3. serves the application
4. makes changes to a new application

> [Setting up local environment](https://angular.io/guide/setup-local)

---

# Create new workspace in an initial application

run this to create a new ng application
```shell
ng new <angular-app>
```

serving the application
```shell
cd <path/to/ang/app>
ng serve --open
```

---

# Tour of heroes initial set up

> So far with the new app, accept all defaults

The main page you see now is the application shell, this is controlled by the component `AppComponent`
> Components are the fundamental building blocks of angular apps.
> They display data on screen, listen for user input and take action based on that input

## Initial changes to the app
First locates the files that makes up the `AppComponent` includes
- `app.component.ts` component class code in ts
- `app.component.html` component template in HTML
- `app.component.css` component private css style

Changing the application title by setting a variable in the class code and reference that in the html
```html
<h1>{{ title }}</h1>
```
```ts
title = 'Tour of heroes'
```

## Application styling
most app aims for a consistent look through out the whole app.
the `ng new` created an empty `styles.css` for this purpose.
put your application wide styles there

---

# Summary
so far
- create initial application with `ng new`
- learn that component can display data
- double curly braces for interpolation to display data

## Further reading
- [Testing](https://angular.io/guide/testing)